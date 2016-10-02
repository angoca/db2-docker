# Supported tags and respective `Dockerfile` links

 * [`expc`, `latest` (install/expc/Dockerfile)](https://github.com/angoca/db2-docker/blob/master/install/expc/Dockerfile)
 * [`10.5-ese`, `ese` (install/10.5/server_t/Dockerfile)](https://github.com/angoca/db2-docker/blob/master/install/10.5/server_t/Dockerfile)

# What is DB2?

IBM DB2 is a family of database server products developed by IBM. These products all support the relational model, but in recent years some products have been extended to support object-relational features and non-relational structures, in particular XML.

Historically and unlike other database vendors, IBM produced a platform-specific DB2 product for each of its major operating systems. However, in the 1990s IBM changed track and produced a DB2 "common server" product, designed with a common code base to run on different platforms.

 * [wikipedia.org/wiki/IBM_DB2](https://en.wikipedia.org/wiki/IBM_DB2)
 * [DB2 LUW](http://www.ibm.com/analytics/us/en/technology/db2/)
 * [DB2 Express-C](http://www.ibm.com/software/data/db2/express-c/download.html)

![DB2 logo](https://raw.githubusercontent.com/angoca/db2-docker/master/install/expc/logo.png)

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

This image will download and install DB2 LUW Express-C, but it will not create an instance nor a database.

NOTE: The [GitHub repository](https://github.com/angoca/db2-docker) has another Docker file that installs [DB2 Enterprise Server Edition](https://github.com/angoca/db2-docker/tree/master/install/10.5/server_t) from the most recent fixpack; however, this installation requires a valid license after 90 days of usage. For this reason, this container is not published in the Hub.

In order to configure the DB2 environment, you can use the image [angoca/db2-instance](https://registry.hub.docker.com/u/angoca/db2-instance/) or you can create yourself the instance (`db2icrt`) and the database (`db2 create db sample`).

The installer is obtained direclty from IBM; however, this link is temporal. If the link is not longer valid, you just need to modify a page of the [Wiki](https://github.com/angoca/db2-docker/wiki/db2-link-expc), by providing a new valid link. The instructions are in the same page, just visit:

 * [DB2 download link page in wiki](https://github.com/angoca/db2-docker/wiki/db2-link-expc)

For the DB2 installation, a provided response file is used. You can clone this repository and modify the response file for your own needs.

DB2 will be installed in the container in:

For Express-C:

    /opt/ibm/db2/V11.1

For ESE:

    /opt/ibm/db2/V10.5

Please, check the [Travis-CI execution](https://travis-ci.org/angoca/db2-docker) to see how this image is build.

## Next steps

You will probably use the default instance `db2inst1` listening on port 50000. You can use the `angoca/db2-instance` in order to prepare the environment for an instance with these characteristics.

 * [`angoca/db2-instance`](https://registry.hub.docker.com/u/angoca/db2-instance/)

If you want to configure the environment by yourself, you can run the container and execute the commands to create the instance (`db2icrt`), the database (`db2 create db xxx`), the security (`useradd`) and the other stuff.

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


