# This Docker file downloads the DB2 LUW binaries and install them in the image.
# It install the necessary libraries.
#
# Version: 2015-01-04
# Author: Andres Gomez Casanova (AngocA)
# Made in COLOMBIA.

FROM ubuntu:14.04

MAINTAINER Andres Gomez <angoca@yahoo.com>

# Set of variables to define the type of DB2 being installed.

## URL to download the installer. From IBM, but it has to be updated because the
## link is temporal. You can get a new valid link from
## http://www.ibm.com/software/data/db2/express-c/download.html
ENV DB2_BIN https://iwm.dhe.ibm.com/sdfdl/v2/regs2/db2pmopn/db2_v105/expc/Xa.2/Xb.aA_60_-i75MwL9JKb3_JnLkeDltZUdcgF5mlWmBo_g/Xc.db2_v105/expc/v10.5_linuxx64_expc.tar.gz/Xd./Xf.LPr.D1vk/Xg.7896296/Xi.swg-db2expressc/XY.regsrvs/XZ.USh1SRvgyXVOj1uqGuKpSQk2Sqg/v10.5_linuxx64_expc.tar.gz
## Name of the downloaded file.
ENV DB2_INSTALLER v10.5_linuxx64_expc.tar.gz
## Directory of the installers. Associated to the edition.
ENV DB2_INST_DIR expc
## Version of the downloaded file. Used for db2prereqcheck.
ENV DB2_VERSION 10.5.0.4
## Name of the response file included in the Docker image.
ENV DB2_RESP_FILE db2expc.rsp

# Updates Linux. Includes i386
RUN dpkg --add-architecture i386 && \
  apt-get update && \
  apt-get install -y \
    aria2 \
    libstdc++6-4.4-pic \
    libaio1 \
    libpam-ldap:i386 \
    lib32stdc++6

# Download the installer.
RUN cd /tmp && \
  aria2c -x 16 ${DB2_BIN}

# Extract the installer and delete the tar file.
RUN cd /tmp && \
  tar -zvxf ${DB2_INSTALLER} && \
  rm ${DB2_INSTALLER}

# Copies the response file
COPY ${DB2_RESP_FILE} /tmp/${DB2_RESP_FILE}

# Install DB2 and remove the installer.
RUN cd /tmp/${DB2_INST_DIR} && \
  ./db2prereqcheck -v ${DB2_VERSION} && \
  ./db2setup -r /tmp/${DB2_RESP_FILE} && \
  cat /tmp/db2setup.log && \
  cd && \
  rm -Rf /tmp/${DB2_INST_DIR}

# Removes the cache of apt-get and the unnecessary packages.
RUN apt-get purge -y aria2 && \
  apt-get clean -y

