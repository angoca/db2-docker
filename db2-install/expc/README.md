## Supported tags and respective `Dockerfile` links

 * [`expc`, `latest` (db2-install/expc/Dockerfile)](https://github.com/angoca/db2-docker/blob/master/install/expc/Dockerfile)
 * [`11.1-ese`, `ese` (db2-install/11.1/server_t/Dockerfile)](https://github.com/angoca/db2-docker/blob/master/db2-install/11.1/server_t/Dockerfile)
 * [`10.5-ese` (db2-install/10.5/server_t/Dockerfile)](https://github.com/angoca/db2-docker/blob/master/db2-install/10.5/server_t/Dockerfile)

## What is DB2?

IBM DB2 is a family of database server products developed by IBM. These products all support the relational model, but in recent years some products have been extended to support object-relational features and non-relational structures, in particular XML.

Historically and unlike other database vendors, IBM produced a platform-specific DB2 product for each of its major operating systems. However, in the 1990s IBM changed track and produced a DB2 "common server" product, designed with a common code base to run on different platforms.

 * [wikipedia.org/wiki/IBM_DB2](https://en.wikipedia.org/wiki/IBM_DB2)
 * [DB2 LUW](http://www.ibm.com/analytics/us/en/technology/db2/)
 * [DB2 Express-C](http://www.ibm.com/software/data/db2/express-c/download.html)

![DB2 logo](https://raw.githubusercontent.com/angoca/db2-docker/master/db2-install/expc/logo.png)

# What is a DB2 instance?

A DB2 instance is a running process that controls the security at the higher level, listens on a specific port, controls the databases it hosts, and many other operations related to database administration.

## Set of images

This image is part of a set of images to create your DB2 environment:

 * [db2-install: Downloads and installs DB2](https://registry.hub.docker.com/u/angoca/db2-install/)
   * [![](https://images.microbadger.com/badges/image/angoca/db2-install.svg)](https://microbadger.com/images/angoca/db2-install "Get your own version badge on microbadger.com")
 * [db2-db2inst1: Instance db2inst1 created](https://registry.hub.docker.com/u/angoca/db2-db2inst1/)
   * [![](https://images.microbadger.com/badges/image/angoca/db2-db2inst1.svg)](https://microbadger.com/images/angoca/db2-db2inst1 "Get your own image badge on microbadger.com")
 * [db2-sample: Database sample created (Without Dockerfile)](https://registry.hub.docker.com/u/angoca/db2-sample/)
   * [![](https://images.microbadger.com/badges/image/angoca/db2-sample.svg)](https://microbadger.com/images/angoca/db2-sample "Get your own version badge on microbadger.com")

This is the stack of images:

    +-----------------+
    | 3) db2-sample   |  <-- Sample database (db2sampl)
    +-----------------+
    | 2) db2-db2inst1 |  <-- Default instance created (db2inst1:50000)
    +-----------------+
    | 1) db2-install  |  <-- DB2 Express-C installed
    +-----------------+

## How to use this image

This image has two parts: the installation of Db2, and the preparation for the instance creation.

# Instalation

This image will download and install DB2 LUW Express-C, but it will not create an instance nor a database.

NOTE: The [GitHub repository](https://github.com/angoca/db2-docker) has another Docker file that installs [DB2 Enterprise Server Edition](https://github.com/angoca/db2-docker/tree/master/db2-install/11.1/server_t) from the most recent fixpack; however, this installation requires a valid license after 90 days of usage. For this reason, this container is not published in the Docker Hub.

The installer is obtained direclty from IBM; however, this link is temporal. If the link is not longer valid, you just need to modify a page of the [Wiki](https://github.com/angoca/db2-docker/wiki/db2-link-expc), by providing a new valid link. You just need to modify the link, by replacing the last line of the wiki. The instructions are in the same page, just visit:

 * [DB2 download link page in wiki Expc - 11.1](https://github.com/angoca/db2-docker/wiki/db2-link-expc)
 * [DB2 download link page in wiki ESE - 11.1](https://github.com/angoca/db2-docker/wiki/db2-link-server_t-11.1)
 * [DB2 download link page in wiki ESE - 10.5](https://github.com/angoca/db2-docker/wiki/db2-link-server_t-10.5)

For the DB2 installation, a provided response file is used. You can clone this repository and modify the response file for your own needs.

DB2 will be installed in the container in:

For Express-C:

    /opt/ibm/db2/V11.1

For ESE:

    /opt/ibm/db2/V11.1
    /opt/ibm/db2/V10.5

Please, check the [Travis-CI execution](https://travis-ci.org/angoca/db2-docker) to see how this image is build.

# Instance creation

This image has a set scripts to ease the instance creation. The script that creates the instance follows the instructions of a response file. The instance by default is `db2inst1` listening on port 50000 installed in the `/home/db2inst1` directory.

Please, check the [Travis-CI execution](https://travis-ci.org/angoca/db2-docker) to see how this image is build.

# Build

The build process can be done via a `pull` or directly from the sources via `build`. This will create the image that will be ready to run.

Pull from Docker:

    sudo docker pull angoca/db2-install:latest

Build from sources

    git clone https://github.com/angoca/db2-docker.git
    sudo docker build install/expc

# Run

The execution of a new container should be done in privilege mode, interactive with a seudo TTY. For example:

    sudo docker run -i -t --privileged=true --name="db2inst1" -p 50000:50000 angoca/db2-install

The name of the container will be `db2inst1`.

You can try the following line in order to not use privileged mode:

    sudo docker run -i -t --ipc="host" --cap-add IPC_LOCK --cap-add IPC_OWNER --name="db2inst1" -p 50000:50000 angoca/db2-install

Once the container is running, the console is active under the `/tmp/db2_conf` directory. In this directory you will find a DB2 response file and a script to create an instance. The DB2 response file is configured to create a DB2 instance called `db2inst1` listening on port `50000`. If you want to change these or other properties, you just need to modify the response file or call the createInstance script with another username, for example:

    ./createInstance

Or for a specific instance name

    ./createInstance myinst

It will run `db2isetup`, and then you can change to the instance user and start the instance. Once there, you can create the database, or perform other configuration changes.

Once you have finished the configuration, you can leave the container running by typing:

    Ctrl + P + Q

# Local file system

If you want to have an independent execution environment, a shared storage, you can mount a local directory in the images. It is recommended that you mount the `/home` directory and create all instances under this structure. This will store the home directories of the instances in the host, instead of in the containers.

    /home <-- /db2 locally in the host
      /db2inst1 <-- Home directory for instance db2inst1
      /db2inst2 <-- Home directory for instance db2inst2

The previous distribution works only if you create different instance users across all containers. (It is not necessary to have one instance per container, but different instances across all containers when using host storage.)

It is very important that you mount this file system before creating the instance.

    sudo mkdir /db2
    sudo docker run -i -t --privileged=true --name="db2inst1" -p 50000:50000 -v /db2:/home angoca/db2-instance

NOTE: If you use automatic storage in DB2, and the database creation does not specify any path, the data will be also stored under `/home`. Instead, if you specify specific paths for your containers, make sure where they are stored (in the containers or in the host via mount).

# Daemon

Once the instance has been created, you can run the DB2 instance as a Docker daemon.

    sudo docker start

Once the container with DB2 is running, it can be used to create, populate, manipulate and perform other activities with databases.

If you want to access the console, you need to do an attach to the container

    sudo attach db2inst1

## Acknowledgements

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

## Advantages of these images

The advantages to use this image instead of the other are:

 * The DB2 binary file is downloaded semi-automatically. The wiki has a valid link and this is the only thing that needs to be modified. The other images requiere to modify the image with a valid link or to have DB2 installer/binaries locally in the machine.
 * This image has a mechanism to create more instances with a simple script that uses a response file. The instance owner can have any name; it is not limited to `db2inst1` or something like `db2instX` where X is a number.
 * The environment can be configured in different ways. It is not limited to a fixed instance or database. The set of images provide different levels of flexible configuration.
 * The images are published in Docker in the `angoca` repository. The image is not created on the fly. The basic images are created from Dockerfiles, the last one was published in the repository with the database already created. As part of the publish, a corresponding documentation is provided.
 * The images can be found by performing a search in Docker. This allows to have a better visibility.
 * It was developed by a DB2 DBA. This makes this image appropriate not only for developers but also for DBAs and SysAdmins.
 * The complete installation and configuration is divided in different images. This makes the solution more flexible and easy to extent.
 * The image tries to be based on recent versions. For example one of the last fixpacks in Db2 v10.5, and the most recent fixpack in v11.1. Also, a recent version of Linux Ubuntu is used; for v11.1 is used Ubuntu 16.04.
 * This image is based on a Linux distribution supported by IBM, which is Ubunut. CentOs is not supported.
 * There is documentation. This is very important for new users to understand the structure of the images.

## User Feedback

# Issues

If you have any problems with or questions about this image, please contact us through a [GitHub issue](https://github.com/angoca/db2-dockers/issues).

You can also reach the mainteiner via Twitter [@angoca](https://twitter.com/angoca).

# Contributing

You are invited to contribute new features, fixes, or updates, large or small; we are always thrilled to receive pull requests, and do our best to process them as fast as we can.

Before you start to code, we recommend discussing your plans through a GitHub issue, especially for more ambitious contributions. This gives other contributors a chance to point you in the right direction, give you feedback on your design, and help you find out if someone else is working on the same thing.


