This document covers how to create a db2instance container with a host Persistent Volume (pv)

## Create a host persistent volume
For my testing I have used minikube, so had to login to vm and create the folder
``` sh
minikube ssh
mkdir /data/pv0001
```

Next create a persistent volume in kubernetes using the yaml below

``` yaml
apiVersion: v1
kind: PersistentVolume
metadata:
  name: pv0001
spec:
  accessModes:
    - ReadWriteOnce
  capacity:
    storage: 20Gi
  hostPath:
    path: /data/pv0001/
```

``` bash
kubectl create -f host_pv.yaml
```

## Create the db2 instance.
The angoca/db2-instance:expc image has an installation of db2 in the /opt directory but no instance of db2, we will create the db2 instance, by first creating the container and then running some commands on the container.

### Create the container with the following yaml
``` yaml
apiVersion: v1
kind: Pod
metadata:
  name: db2-instance
  labels:
    tier: db2-database
spec:
  volumes:
    - name: db2-data-dir
      hostPath:
        path: /data/pv0001/
  containers:
  - name: db2-instance
    image: angoca/db2-instance:expc
    command: ["/bin/sh"]
    args: ["-c", "while true; do echo hello; sleep 10;done"]
    ports:
      - containerPort: 50000
    volumeMounts:
      - mountPath: /home
        name: db2-data-dir
    securityContext:
      privileged: true
```
``` bash
kubectl create -f pod-angoca-db2-instance.yaml
#ssh to the container
kubectl exec -it db2-angoca-mount bash
root@db2-angoca-mount:$ cd /tmp/db2_conf/
root@db2-angoca-mount:/tmp/db2_conf$./createInstance
root@db2-angoca-mount:/tmp/db2_conf$ su - db2inst1
db2inst1@db2-angoca-mount:~$ db2sampl
db2inst1@db2-angoca-mount:~$ exit
root@db2-angoca-mount:/tmp/db2_conf$ exit

```

The above commands will create the db2 storage files in /home/db2inst1 directory which is actually the pv from the host. Due to this our database data will be persisted across container deletions. We also create a sample db to test connections.

### Forward ports from your local host
``` shell
kubectl port-forward db2-instance 50000:50000
```

Test to make sure you can connect to the db using your favorite database tool.

### Delete the pod
``` bash
kubectl delete -f pod-angoca-db2-instance.yaml
```


## Create a new container from the db2inst image with a mounted volume.

There is another image in the angoca repo that has an instance alrady created, we use this image now but with the data of the mounted volume from the previous step.

### Create a container with the following yaml.

``` yaml
apiVersion: v1
kind: Pod
metadata:
  name: db2-angoca-mount
  labels:
    tier: db2-database
spec:
  volumes:
    - name: db2-data-dir
      hostPath:
        path: /data/pv0001/
  containers:
  - name: db2-angoca-mount-container
    image: angoca/db2inst1:expc
    command: ["/bin/sh"]
    args: ["-c", "/home/db2inst1/sqllib/adm/db2start;while true; do echo hello; sleep 10;done"]
    ports:
      - containerPort: 50000
    volumeMounts:
      - mountPath: /home
        name: db2-data-dir
    securityContext:
      privileged: true

```
``` bash
kubectl create -f pod-angoca-db2inst1-mount.yaml
#forward the ports
kubectl port-forward db2-angoca-mount 50000:50000
```

Thats it!! You should be all set to use this db2 pod from your machine which is running minikube. Try inserting data in some tables, and then destroying the pod and recreating it. The data should be present in the new pod that is created.You can also login to the minikube vm and check contents of the directory, you should see something like below.

``` bash
C:\Users\mahesh_sawaiker>minikube ssh
                         _             _
            _         _ ( )           ( )
  ___ ___  (_)  ___  (_)| |/')  _   _ | |_      __
/' _ ` _ `\| |/' _ `\| || , <  ( ) ( )| '_`\  /'__`\
| ( ) ( ) || || ( ) || || |\`\ | (_) || |_) )(  ___/
(_) (_) (_)(_)(_) (_)(_)(_) (_)`\___/'(_,__/'`\____)

$ ls /data
pv0001
$ ls /data/pv0001
db2fenc1  db2inst1
```
