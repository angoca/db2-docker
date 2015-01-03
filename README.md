db2-dockers
===========

# Overview & links

This image will download and install DB2 LUW Express-C.
DB2 is a relational database manager system (RDBMS) from IBM.
It exists in different platforms, including Linux, UNIX and Windows (LUW).
There are several editions of this RDBMS, one of them is free to use.
The most recent version of DB2 is 10.5,

 * [Wikipedia DB2](https://en.wikipedia.org/wiki/IBM_DB2)
 * [DB2 LUW](http://www.ibm.com/software/data/db2/)
 * [DB2 Express-C](http://www.ibm.com/software/data/db2/express-c/download.html)

The binary installer is obtained from a dowcker account.
However, it can be change to get directly from IBM.
The issue with a permanent link to IBM is that it is temporal.

 * Temporal link from [IBM](https://iwm.dhe.ibm.com/sdfdl/v2/regs2/db2pmopn/db2_v105/expc/Xa.2/Xb.aA_60_-i75MwLycnAcDm34-Rpkd7iPiwBl5dXV2dsg/Xc.db2_v105/expc/v10.5_linuxx64_expc.tar.gz/Xd./Xf.LPr.D1vk/Xg.7895377/Xi.swg-db2expressc/XY.regsrvs/XZ.IDHvhZPPvIFxusUn-kAGX-Mv1qU/v10.5_linuxx64_expc.tar.gz)
 * [Installer from Dropbox](https://www.dropbox.com/s/ut3136498v8lbti/v10.5_linuxx64_expc.tar.gz)

The image will just install DB2 and it will not create any DB2 instance.

The [Docker file](https://github.com/angoca/db2-dockers/blob/master/10.5/Dockerfile.md)

# How-to/usage

TODO Just pull this image, and DB2 will be installed in the container in:

    /opt/ibm/db2/V10.5

# Issues & contributions

In you find any issue, please contact @angoca
