# Supported tags and respective `Dockerfile` links

 * [`instance-expc`, `latest` (instance/expc/Dockerfile)](https://github.com/angoca/db2-docker/blob/master/instance/expc/Dockerfile)
 * [`instance-ese` (instance/server_t/Dockerfile)](https://github.com/angoca/db2-docker/blob/master/instance/server_t/Dockerfile)

# What is DB2?

IBM DB2 is a family of database server products developed by IBM. These products all support the relational model, but in recent years some products have been extended to support object-relational features and non-relational structures, in particular XML.

Historically and unlike other database vendors, IBM produced a platform-specific DB2 product for each of its major operating systems. However, in the 1990s IBM changed track and produced a DB2 "common server" product, designed with a common code base to run on different platforms.

 * [wikipedia.org/wiki/IBM_DB2](https://en.wikipedia.org/wiki/IBM_DB2)
 * [DB2 LUW](http://www.ibm.com/analytics/us/en/technology/db2/)
 * [DB2 Express-C](http://www.ibm.com/software/data/db2/express-c/download.html)

![DB2 logo](https://raw.githubusercontent.com/angoca/db2-docker/master/install/expc/logo.png)

## What is a DB2 instance?

A DB2 instance is a running process that controls the security at the higher level, listens on a specific port, controls the databases it hosts, and many other operations related to database administration.

# Set of images

This image is part of a set of images to create your DB2 environment:

 * [db2-install: Downloads and installs DB2/](https://registry.hub.docker.com/u/angoca/db2-install/)
 * [db2-instance: Configures the environment to create an instance](https://registry.hub.docker.com/u/angoca/db2-instance/)
 * [db2inst1: Instance db2inst1 created (Without Dockerfile)](https://registry.hub.docker.com/u/angoca/db2inst1/)
 * [db2-sample: Database sample created (Without Dockerfile)](https://registry.hub.docker.com/u/angoca/db2-sample/)

This is the stack of images:

    +----------------+
    |   db2-sample   |  <-- Sample database (db2sampl)
    +----------------+
    |    db2inst1    |  <-- Default instance created (db2inst1:50000)
    +----------------+
    |  db2-instance  |  <-- Environment to create an instance
    +----------------+
    |   db2-install  |  <-- DB2 Express-C installed
    +----------------+

# How to use this image

This image will prepare the environment to create a DB2 instance. It uses the [`angoca/db2-install`](https://registry.hub.docker.com/u/angoca/db2-install/) image that installs DB2.

Once the installation was done, this image could be loaded. This image will populate the previous image with some scripts to ease the instance creation. The process follows the instructions of a response file. The instance by default is `db2inst1` listening on port 50000 installed in the `/home/db2inst1i` directory.

The process is performed in two steps:

 * First, the image is filled with the necessary scripts (build).
 * Second, the image creates the instance interactively and start it in background (run).

Please, check the [Travis-CI execution](https://travis-ci.org/angoca/db2-docker) to see how this image is build.

## Build

The build process can be done via a `pull` or directly from the sources via `build`. This will create the image that will be ready to run.

Pull from Docker:

    sudo docker pull angoca/db2-instance:latest

Build from sources

    git clone https://github.com/angoca/db2-docker.git
    sudo docker build instance/expc

## Run

The execution of a new container should be done in privilege mode, interactive
with a seudo TTY.
For example:

    sudo docker run -i -t --privileged=true --name="db2inst1" -p 50000:50000 angoca/db2-instance

The name of the container will be `db2inst1`.

You can try the following line in order to not use privileged mode:

    sudo docker run -i -t --ipc="host" --cap-add IPC_LOCK --cap-add IPC_OWNER --name="db2inst1" -p 50000:50000 angoca/db2-instance

Once the container is running, the console is active under the `/tmp/db2_conf` directory. In this directory you will find a DB2 response file and a script to create an instance. The DB2 response file is configured to create a DB2 instance called `db2inst1` listening on port `50000`. If you want to change these or other properties, you just need to modify the response file or call the createInstance script with another username, for example:

    createInstance myinst

It will run `db2isetup`, then start the instance, and leave the console open under the `db2inst1` user or the one your provided. Once there, you can create the database, or perform other configuration changes.

    ./createInstance

Once you have finished the configuration, you can leave the container running by typing:

    Ctrl + P + Q

## Local file system

If you want to have an independent execution environment, but a shared storage, you can mount a local directory in the images. It is recommended that you mount the `/home` directory and create all instances under this structure. This will store the home directories of the instances in the host, instead of in the containers.

    /home <-- /db2 locally in the host
      /db2inst1 <-- Home directory for instance db2inst1
      /db2inst2 <-- Home directory for instance db2inst2

The previous distribution works only if you create different instance users across all containers. (It is not necessary to have one instance per container, but different instances across all containers when using host storage.)

It is very important that you mount this file system before creating the instance.

    sudo mkdir /db2
    sudo docker run -i -t --privileged=true --name="db2inst1" -p 50000:50000 -v /db2:/home angoca/db2-instance

NOTE: If you use automatic storage in DB2, and the database creation does not specify any path, the data will be also stored under `/home`. Instead, if you specify specific paths for your containers, make sure where they are stored (in the containers or in the host via mount).

## Daemon

Once the instance has been created, you can run the DB2 instance as a Docker daemon.

    sudo docker start

Once the container with DB2 is running, it can be used to create, populate, manipulate and perform other activities with databases.

If you want to access the console, you need to do an attach to the container

    sudo attach db2inst1

# Acknowledgements

The design of this image is based on the following DB2-Docker images:

 * [grange74/docker-db2](https://github.com/grange74/docker-db2) - https://registry.hub.docker.com/u/grange74/db2/
 * [bryantsai/db2-docker](https://github.com/bryantsai/db2-docker)
 * [jeffbonhag/db2-docker](https://github.com/jeffbonhag/db2-docker)
 * [miraitechno/db2](https://github.com/miraitechno/docker-db2) - https://registry.hub.docker.com/u/miraitechno/db2/
 * https://registry.hub.docker.com/u/zongqiang/db2v10.5expc/
 * [IBM IM C3ofC - DB2](https://github.com/IMC3ofC/db2express-c.docker)
 * [https://hub.jazz.net/project/cbmcgee/rtcdocker/overview](https://hub.jazz.net/project/cbmcgee/rtcdocker/overview#https://hub.jazz.net/project/cbmcgee/rtcdocker/cbmcgee%2520%257C%2520rtcdocker/_7MYIkF4LEeSi-OIwg-tlIA/_7Mut4F4LEeSi-OIwg-tlIA/db2/db/Dockerfile) Chris McGee

And the posts of the following blogs:

 * [DB2 on Docker](https://bryantsai.com/db2-on-docker/)
 * [db2indocker](http://db2indocker.blogspot.com.co/)

# Advantages of these images

The advantages to use this image instead of the other are:

 * The DB2 binary file is download semi-automatically. Just the wiki has to have the valid link. The other images requiere to modify the image with a valid link or to have DB2 installer/binaries locally in the machine.
 * This image has a mechanism to create more instances with a simple script that uses a response file. The instance owner can have any name; it is not limited to `db2inst1` or something like `db2instX` where X is a number.
 * The environment can be configured in different ways. It is not limited to a fixed instance or database. The set of images provide different levels of flexible configuration.
 * The images are published in Docker in the `angoca` repository. The image is not created on the fly. The basic images are created from Dockerfiles, the other were published in the repository with the instance or database already created. As part of the publish, a corresponding documentation is provided.
 * The images can be found by performing a search in Docker. This allows to have a better visibility.
 * It was developed by a DB2 DBA. This makes this image appropriate not only for developers but also for DBAs and SysAdmins.
 * The complete installation and configuration is divided in different images. This makes the solution more flexible and easy to extent.
 * There is documentation. This is very important for new users to understand the structure of the
   images.

# User Feedback

## Issues

If you have any problems with or questions about this image, please contact us through a [GitHub issue](https://github.com/angoca/db2-dockers/issues).

You can also reach the mainteiner via Twitter [@angoca](https://twitter.com/angoca).

## Contributing

You are invited to contribute new features, fixes, or updates, large or small; we are always thrilled to receive pull requests, and do our best to process them as fast as we can.

Before you start to code, we recommend discussing your plans through a GitHub issue, especially for more ambitious contributions. This gives other contributors a chance to point you in the right direction, give you feedback on your design, and help you find out if someone else is working on the same thing.


