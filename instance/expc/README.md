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
the [`angoca/db2-install`](https://registry.hub.docker.com/u/angoca/db2-install/)
image.

Once the installation was done, this image could be loaded.
This will populate the image with some scripts to ease the instance creation.
The process follows the instructions of a response file.
The instance by default is `db2inst1` with port 50000 in
`/home/db2inst1i` directory.

The process is performed in two steps:

 * First, the image is filled with the necessary scripts (build).
 * Second, the image creates the instance interactively (run).

There is a third step that is the execution of the instance as a daemon.

## Build

The build process can be done via a `pull` or directly from the sources via
`build`.
This will create the image that will be ready to run.

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

Once the container is running, the console is active under the `/tmp/db2_conf`
directory.
In this directory you will find a DB2 response file and a script to create an
instance.
The DB2 response file is configured to create a DB2 instance called `db2inst1`
listening on port `50000`.
If you want to change these or other properties, you just need to modify the
response file.

Once the response file is ready, you just need to execute the script.
It will run `db2isetup`, then start the instance, and leave the console open
under the `db2inst1` user.
There, you can create the database, or perform other configuration changes.

    ./createInstance

Once you have finish the configuration, you can leave the container running by
typing:

    Ctrl + P + Q

## Local file system

If you want to have an independent execution environment, but a shared storage,
you can mount a local directory in the images.
It is recommended that you mount the `/home` directory and create all instances
under this structure.
This will store the home directories of the instances in the local host,
instead of in the containers.

    /home <-- /db2 locally in the host
      /db2inst1 <-- Home directory for instance db2inst1
      /db2inst2 <-- Home directory for instance db2inst2

The previous distribution works only if you create different instance users
across all containers.
(It is not necessary to have one instance per container, but different
instances across all containers.)

It is very important that you mount this file system before creating the
instance.

    sudo mkdir /db2
    sudo docker run -i -t --privileged=true --name="db2inst1" -p 50000:50000 -v /db2:/home angoca/db2-instance

If you use automatic storage in DB2, and the database creation does not
specify any path, the data will be also stored under `/home`.
Instead, if you specify specific paths for your containers, make sure where
they are stored (in the containers or in the host via mount).

## Daemon

Once the instance has been created, you can run the DB2 instance as a Docker
daemon.

    sudo docker start

If you want to access the console, you need to do an attach to the container

    sudo attach db2inst1

# User Feedback

## Issues

If you have any problems with or questions about this image, please contact us
through a [GitHub issue](https://github.com/angoca/db2-docker/issues).

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

