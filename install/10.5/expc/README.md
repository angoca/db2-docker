# Supported tags and respective `Dockerfile` links

 * [`10.5-expc`, `expc`, `latest` (10.5/expc/Dockerfile)](https://github.com/angoca/db2-docker/blob/master/install/10.5/expc/Dockerfile)
 * [`10.5-server_t`, `server_t` (10.5/server_t/Dockerfile)](https://github.com/angoca/db2-docker/blob/master/install/10.5/server_t/Dockerfile)

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
 * [DB2 LUW](http://www.ibm.com/analytics/us/en/technology/db2/)
 * [DB2 Express-C](http://www.ibm.com/software/data/db2/express-c/download.html)

![DB2 logo](https://raw.githubusercontent.com/angoca/db2-docker/master/install/10.5/expc/logo.png)

# How to use this image

This image will download and install DB2 LUW Express-C, but it will not create
and instance nor database.

In order to configure the DB2 environment, you can use the image
[angoca/db2-instance](https://registry.hub.docker.com/u/angoca/db2-instance/)
or you can create yourself the instance (`db2icrt`) and the database (
`db2 create db sample`).

The installer is obtained direclty from IBM; however, this link is temporal.
If the link is not longer valid, you just need to change a page of the Wiki,
by providing a new valid link.
The instruction are in the same page:

 * [DB2 download link page in wiki](https://github.com/angoca/db2-docker/wiki/db2-link-expc)

For the DB2 installation, a provided response file is used.
You can clone this repository and modify the response file for your own needs.

DB2 will be installed in the container in:

    /opt/ibm/db2/V10.5

## Next steps

You will probably use the default instance `db2inst1` listening on port 50000.
You can use the `angoca/db2-instance` in order to prepare the environment for
an instance with these characteristics.

 * [`angoca/db2-instance`](https://registry.hub.docker.com/u/angoca/db2-instance/)

If you want to configure the environment by yourself, you can run the container
and execute the commands to create the instance (`db2icrt`), the database
(`db2 create db xxx`), the security (`useradd`) and the rest.

## Set of images

This image is part of a set of images to create your DB2 environment:

    +----------------+
    |   db2-sample   |  <-- Sample database (db2sampl)
    +----------------+
    |    db2inst1    |  <-- Default instance created (db2inst1:50000)
    +----------------+
    |  db2-instance  |  <-- Environment to create an instance
    +----------------+
    |   db2-install  |  <-- DB2 Express-C installed
    +----------------+

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

