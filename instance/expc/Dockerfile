# This Docker file downloads the DB2 LUW binaries and install them in the image.
# It install the necessary libraries.
#
# Version: 2015-01-04
# Author: Andres Gomez Casanova (AngocA)
# Made in COLOMBIA.

FROM angoca/db2-install:latest

MAINTAINER Andres Gomez <angoca@yahoo.com>

# Set of variables to define the type of DB2 being installed.

## Name of the response file included in the Docker image.
ENV DB2_RESP_FILE db2expc.rsp
## Directory where DB2 is installed.
ENV DB2_DIR /opt/ibm/db2/V10.5

# Copies the response file
COPY ${DB2_RESP_FILE} /tmp/${DB2_RESP_FILE}


cat /tmp/db2isetup.log
