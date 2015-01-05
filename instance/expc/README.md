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

# Issues & contributions

In you find any issue, please contact [@angoca](https://twitter.com/angoca).
Or create an issue at
[https://github.com/angoca/db2-dockers/issues](https://github.com/angoca/db2-dockers/issues)

