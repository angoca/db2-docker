# Overview & links

This image will prepare the environment to create a DB2 instance.
This image uses angoca/db2-install.

The Dockefile can be found at:
[https://raw.githubusercontent.com/angoca/db2-docker/master/instance/expc/Dockerfile](https://raw.githubusercontent.com/angoca/db2-docker/master/instance/expc/Dockerfile)

# How-to/usage

Once the installation was done, this image could be loaded.
This will populate the image with some scripts to ease the instance creation.
The process follows the instruction of a reponse file.
The instance by default is `db2inst1` with port 50000 in
`/home/db2inst1 directory`.

The process is performed in two steps:

 * First, the image is filled with the necessary scripts (build).
 * Second, the image creates the instance interactively (run).

There is a third step that is the execution of the instance as a daemon.

## Build

The build process can be done via a `pull` or directly from the sources via
`build`.
This will create the image that will be ready to run.

## Run

The execution of a new container should be done in privilege mode, interactive
with a seudo TTY.
For example:

    sudo docker run -i -t --privileged=true --name="db2inst1" angoca/db2-instance

The name of the container will be `db2inst1`.

Once the container is running, the console is active under the `/tmp/db2_conf`
directory.
In this directory you will find a DB2 response file and a script to create an
instance.
The DB2 response file is configured to create a DB2 instance called `db2inst1`
listening on port `50000`. If you want to change these or other properties, you
just need to modify the response file.

Once the response file is ready, you just need to execute the script.
It will run `db2isetup`, then start the instance, and leave the consolse open
under the `db2inst1` user.
There, you can create the database, or perform other changes.

    ./createInstance

## Daemon

Once the instance has been created, you can run the DB2 instance as a Docker
daemon.

    sudo docker run -d -p 50000:50000 

# Issues & contributions

In you find any issue, please contact [@angoca](https://twitter.com/angoca).
Or create an issue at
[https://github.com/angoca/db2-dockers/issues](https://github.com/angoca/db2-dockers/issues)

