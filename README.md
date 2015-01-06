This is a set of Docker images to install DB2 LUW.
The repository consist of two sets of images:

 * db2-install: Download and install DB2/
 * db2-instance: Configures the environment to create an instance.

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

In you find any issue, please contact [@angoca](https://twitter.com/angoca).

