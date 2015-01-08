This is a set of Docker images to install DB2 LUW.
The repository consist of two sets of images:

 * [db2-install: Download and install DB2/](https://registry.hub.docker.com/u/angoca/db2-install/)
 * [db2-instance: Configures the environment to create an instance](https://registry.hub.docker.com/u/angoca/db2-instance/)

This can install DB2 Express-C or Enterprise Server Trial edition.
The links to download these products are temporal, and they have to be
updated in the `Dockerfile`.

 * [DB2 LUW](http://www.ibm.com/software/data/db2/)
 * [DB2 Express-C](http://www.ibm.com/software/data/db2/express-c/download.html)

The first image will prepare the DB2 environment, by just installing the
binaries.
After that, the user can start the configuraiton with  the second image, that
gives a set of script to create the instance and configure the default values.
These values can be modified for other configurations.

This image was based on three existing DB2-Docker images:

 * [grange74/docker-db2](https://github.com/grange74/docker-db2) - https://registry.hub.docker.com/u/grange74/db2/
 * [bryantsai/db2-docker](https://github.com/bryantsai/db2-docker)
 * [jeffbonhag/db2-docker](https://github.com/jeffbonhag/db2-docker)
 * [miraitechno/db2](https://github.com/miraitechno/docker-db2) - https://registry.hub.docker.com/u/miraitechno/db2/
 * https://registry.hub.docker.com/u/zongqiang/db2v10.5expc/

The advantages to use this image instead of the other are:

 * The DB2 binary file is download semi-automatically.
   Just the wiki has to have the valid link.
   The other images requiere to modify the image with a valid link or to have
   DB2 installer locally in the machine.
 * This image has a mechanism to create more instances with a simple script
   that uses a response file.
   The instance owner can have any name; it is not limited to `db2inst1` or
   something like `db2instX` where X is a number.
 * The environment is configured as any other DB2 installation.
   There is not a database, just a running instance.
 * This image is published in Docker, and it is in the `angoca` repository.
   The image is not created on the fly, but it has been built by docker.
   As part of the publish, a corresponding documentation is provided.
 * This image can be found by performing a search in Docker.
   This allows to have a better visibility.
 * It was developed by a DB2 DBA.
   This makes this image appropriate not only for developers but also for DBAs
   and SysAdmins.
 * The complete installation and configuration is divided in two type of
   image.
   This makes the solution more flexible and easy to extent.

In you find any issue, please contact [@angoca](https://twitter.com/angoca).

