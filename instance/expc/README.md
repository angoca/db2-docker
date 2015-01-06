# Supported tags and respective `Dockerfile` links

 * [`instance-expc`, `instance`, `latest` (instance/expc/Dockerfile)](https://github.com/angoca/db2-docker/blob/master/instance/expc/Dockerfile)
 * [`instance-server_t` (instance/server_t/Dockerfile)](https://github.com/angoca/db2-docker/blob/master/instance/server_t/Dockerfile)

# What is DB2?

IBM DB2 is a family of database server products developed by IBM.
These products all support the relational model, but in recent years some
products have been extended to support object-relational features and
non-relational structures, in particular XML.

Historically and unlike other database vendors, IBM produced a
platform-specific DB2 product for each of its major operating systems.
However, in the 1990s IBM changed track and produced a DB2 "common server"
product, designed with a common code base to run on different platforms.

 * [wikipedia.org/wiki/IBM_DB2](https://en.wikipedia.org/wiki/IBM_DB2)
 * [DB2 LUW](http://www.ibm.com/software/data/db2/)
 * [DB2 Express-C](http://www.ibm.com/software/data/db2/express-c/download.html)

![DB2 logo](https://raw.githubusercontent.com/angoca/db2-docker/master/install/10.5/expc/logo.png)

## What is a DB2 instance?

A DB2 instance is a running process that control the security at the higher
level, listens on a specific port, controls the databases that it hosts, and
many other operations related to database administration.

# How to use this image

This image will prepare the environment to create a DB2 instance, and it uses
the `angoca/db2-install` image.

Once the installation was done, this image could be loaded.
This will populate the image with some scripts to ease the instance creation.
The process follows the instruction of a response file.
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


This image will download and install DB2 LUW Express-C, but it will not create
and instance nor database.

In order to configure the DB2 environment, you can use the image
[angoca/db2-instance](https://registry.hub.docker.com/u/angoca/db2-instance/)
or you can create yourself the instance (`db2icrt`) and the database (
`db2 create db sample`).

The installer is obtained direclty from IBM; however, this link is temporal.
You can clone this repository and change the URL for a public Dropbox:

 * [https://www.dropbox.com/s/ut3136498v8lbti/v10.5_linuxx64_expc.tar.gz](https://www.dropbox.com/s/ut3136498v8lbti/v10.5_linuxx64_expc.tar.gz)

Or update the link from:

 * [http://www.ibm.com/software/data/db2/express-c/download.html](http://www.ibm.com/software/data/db2/express-c/download.html)


For the DB2 installation, a provided response file is used.
You can clone this repository and modify the response file for your own needs.

DB2 will be installed in the container in:

    /opt/ibm/db2/V10.5

## Next steps

You will probably use the default instance `db2inst1 listening port 50000.
You can use the `angoca/db2-instance` in order to prepare the environment for
an instance with these characteristics.

 * [`angoca/db2-instance`](https://registry.hub.docker.com/u/angoca/db2-instance/)

# User Feedback

## Issues

If you have any problems with or questions about this image, please contact us
through a [GitHub issue](https://github.com/angoca/db2-dockers/issues).

You can also reach the mainteiner via Twitter
[@angoca](https://twitter.com/angoca).

## Contributing

You are invited to contribute new features, fixes, or updates, large or small;
we are always thrilled to receive pull requests, and do our best to process them
as fast as we can.

Before you start to code, we recommend discussing your plans through a GitHub
issue, especially for more ambitious contributions.
This gives other contributors a chance to point you in the right direction,
give you feedback on your design, and help you find out if someone else is
working on the same thing.

