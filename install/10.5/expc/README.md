# Overview & links

This image will download and install DB2 LUW Express-C.
DB2 is a relational database manager system (RDBMS) from IBM.
It exists in different platforms, including Linux, UNIX and Windows (LUW).
There are several editions of this RDBMS, one of them is free to use, which is
DB2 Express-C edition.
The most recent version of DB2 LUW is 10.5,

 * [Wikipedia DB2](https://en.wikipedia.org/wiki/IBM_DB2)
 * [DB2 LUW](http://www.ibm.com/software/data/db2/)
 * [DB2 Express-C](http://www.ibm.com/software/data/db2/express-c/download.html)

The binary is obtained direclty from IBM; however, this link is temporal.
You can change the URL for a public Dropbox:

 * [https://www.dropbox.com/s/ut3136498v8lbti/v10.5_linuxx64_expc.tar.gz](https://www.dropbox.com/s/ut3136498v8lbti/v10.5_linuxx64_expc.tar.gz)

Or update the link from:

 * [http://www.ibm.com/software/data/db2/express-c/download.html](http://www.ibm.com/software/data/db2/express-c/download.html)

The image will just install DB2 and it will not create any DB2 instance.

List of Docker files:

* [DB2 Express-C 10.5](https://github.com/angoca/db2-dockers/blob/master/install/10.5/expc/Dockerfile)
(expc, latest).
* [DB2 Enterprise server 10.5](https://github.com/angoca/db2-dockers/blob/master/install/10.5/server_t/Dockerfile)
(server_t) trial for 30 days

As you can see, there is another image that will download a DB2 fixpack. This is
valid for 30 days at least you have a license.

For the DB2 installation, a provided response file is used in each case.

# How-to/usage

You just need to call this image, and this will download and install DB2, and
clean the environment. If the binaries cannot be retrieved, the DB2 link can be
changed.
DB2 will be installed in the container in:

    /opt/ibm/db2/V10.5

Remember that the installation does not include any instance or database.

# Issues & contributions

In you find any issue, please contact [@angoca](https://twitter.com/angoca).
Or create an issue at
[https://github.com/angoca/db2-dockers/issues](https://github.com/angoca/db2-dockers/issues)

