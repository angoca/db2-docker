# Supported tags and respective `Dockerfile` links

 * [`expc`, `latest` (db2inst1/expc/Dockerfile)](https://github.com/angoca/db2-docker/blob/master/db2inst1/expc/Dockerfile)
 * [`ese` (db2inst1/server_t/Dockerfile)](https://github.com/angoca/db2-docker/blob/master/db2inst1/server_t/Dockerfile)

# What is DB2?

IBM DB2 is a family of database server products developed by IBM. These products all support the relational model, but in recent years some products have been extended to support object-relational features and non-relational structures, in particular XML.

Historically and unlike other database vendors, IBM produced a platform-specific DB2 product for each of its major operating systems. However, in the 1990s IBM changed track and produced a DB2 "common server" product, designed with a common code base to run on different platforms.

 * [wikipedia.org/wiki/IBM_DB2](https://en.wikipedia.org/wiki/IBM_DB2)
 * [DB2 LUW](http://www.ibm.com/analytics/us/en/technology/db2/)
 * [DB2 Express-C](http://www.ibm.com/software/data/db2/express-c/download.html)

![DB2 logo](https://raw.githubusercontent.com/angoca/db2-docker/master/db2inst1/expc/logo.png)

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

This image creates a DB2 instance based on the scripts that prepares the environment in the previous image. It uses the [`angoca/db2-instance`](https://registry.hub.docker.com/u/angoca/db2-instance/) image that prepares the environment to create instances.

The container provides a created instance with the `db2inst1` user and listening on port `50000` with home directory `/home/db2inst1`. These instructions are provided from the response file of the previous image and the whole process is performed from ./createInstance script.

Once the instance is created, the container can be executed but it needs to be run in privileged mode because a DB2 instance requieres extra permissions to be run.

    sudo docker run -i -t --privileged=true --name="db2inst1" -p 50000:50000 angoca/db2inst1

The name of the container will be `db2inst1`.

Depending on your configuration, you can try the following line in order to not use privileged mode but only the necessary elements for DB2:

    sudo docker run -i -t --ipc="host" --cap-add IPC_LOCK --cap-add IPC_OWNER --name="db2inst1" -p 50000:50000 angoca/db2-instance

Please, check the [Travis-CI execution](https://travis-ci.org/angoca/db2-docker) to see how this image is build.

Once you have finished the configuration, you can leave the container running by typing:

    Ctrl + P + Q

## Next steps

Now, you can create a database and start using DB2:

    su - db2inst1
    db2 create db mydb

If the db2 command is not accepted, it is because the db2profile is not loaded. You can reload the profile with the following command:

    . ~db2inst1/sqllib/db2profile

Take a look that there is a space between the dot and the file name, this is because we are using the source command.

Also, you can create the Sample database and play with a database already populated with data.

    su - db2inst1
    db2sampl

**Note**: For more information please take a look at the documentation of the db2-instance image in Docker Hub. It has more details about shared storage and ackowledgements to all the people that have helped to create these images.

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


