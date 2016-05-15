This is a set of Docker images to install DB2 LUW.
The repository consist in a set of four images:

 * [db2-install: Download and install DB2/](https://registry.hub.docker.com/u/angoca/db2-install/)
 * [db2-instance: Configures the environment to create an instance](https://registry.hub.docker.com/u/angoca/db2-instance/)
 * [db2inst1 (Without Dockerfile)](https://registry.hub.docker.com/u/angoca/db2inst1/)
 * [db2-sampe (Without Dockerfile)](https://registry.hub.docker.com/u/angoca/db2-sample/)

Stack of images:

           expc         server_t
    +----------------+
    |   db2-sample   |               <-- Sample database (db2sampl)
    +----------------+------------+
    |    db2inst1    |            |  <-- Default instance created (db2inst1:50000)
    +----------------+  instance  |
    |  db2-instance  |            |  <-- Environment to create an instance
    +----------------+------------+
    |   db2-install  |  install   |  <-- DB2 Express-C installed
    +----------------+------------+

The install images can install DB2 Express-C or Enterprise Server Trial edition.
The links to download these products are temporal, and they have to be
updated in the Wiki.
The updated link will be used by the images

 * [DB2 LUW](http://www.ibm.com/software/data/db2/)
   ([Wiki](https://github.com/angoca/db2-docker/wiki/db2-link-expc))
 * [DB2 Express-C](http://www.ibm.com/software/data/db2/express-c/download.html)
   ([Wiki](https://github.com/angoca/db2-docker/wiki/db2-link-server_t))

The first image will prepare the DB2 environment, by just installing the
binaries.
After that, the user can start the configuraiton with  the second image, that
gives a set of script to create the instance and configure the default values.
These values can be modified for other configurations.

# Acknowledgements

This image was based on the following DB2-Docker images:

 * [grange74/docker-db2](https://github.com/grange74/docker-db2) - https://registry.hub.docker.com/u/grange74/db2/
 * [bryantsai/db2-docker](https://github.com/bryantsai/db2-docker)
 * [jeffbonhag/db2-docker](https://github.com/jeffbonhag/db2-docker)
 * [miraitechno/db2](https://github.com/miraitechno/docker-db2) - https://registry.hub.docker.com/u/miraitechno/db2/
 * https://registry.hub.docker.com/u/zongqiang/db2v10.5expc/
 * [https://hub.jazz.net/project/cbmcgee/rtcdocker/overview](https://hub.jazz.net/project/cbmcgee/rtcdocker/overview#https://hub.jazz.net/project/cbmcgee/rtcdocker/cbmcgee%2520%257C%2520rtcdocker/_7MYIkF4LEeSi-OIwg-tlIA/_7Mut4F4LEeSi-OIwg-tlIA/db2/db/Dockerfile) Chris McGee

# Advantages of these images

The advantages to use this image instead of the other are:

 * The DB2 binary file is download semi-automatically.
   Just the wiki has to have the valid link.
   The other images requiere to modify the image with a valid link or to have
   DB2 installer locally in the machine.
 * This image has a mechanism to create more instances with a simple script
   that uses a response file.
   The instance owner can have any name; it is not limited to `db2inst1` or
   something like `db2instX` where X is a number.
 * The environment can be configured in different ways.
   It is not limited to a fixed instance or database.
   The set of images provide different levels of flexible configuration.
 * The images are published in Docker in the `angoca` repository.
   The image is not created on the fly.
   The basic images are created from Dockerfiles, the other wer published
   in hte repository with the instance or database already created.
   As part of the publish, a corresponding documentation is provided.
 * The images can be found by performing a search in Docker.
   This allows to have a better visibility.
 * It was developed by a DB2 DBA.
   This makes this image appropriate not only for developers but also for DBAs
   and SysAdmins.
 * The complete installation and configuration is divided in different images.
   This makes the solution more flexible and easy to extent.

In you find any issue, please contact [@angoca](https://twitter.com/angoca) or
create a an issue in [GitHub](https://github.com/angoca/db2-docker/issues).

