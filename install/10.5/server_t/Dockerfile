# This Docker file downloads the DB2 LUW binaries and install them in the image.
# It install the necessary libraries.
#
# This Docker is designed to download a fixpack and install DB2 from it.
#
# Version: 2015-01-04
# Author: Andres Gomez Casanova (AngocA)
# Made in COLOMBIA.

FROM ubuntu:14.04

MAINTAINER Andres Gomez <angoca@yahoo.com>

# Set of variables to define the type of DB2 being installed.

## Name of the downloaded file.
ENV DB2_INSTALLER v10.5fp5_linuxx64_server_t.tar.gz
## Directory of the installers. Associated to the edition.
ENV DB2_INST_DIR server_t
## Version of the downloaded file. Used for db2prereqcheck.
ENV DB2_VERSION 10.5.0.5
## Name of the response file included in the Docker image.
ENV DB2_RESP_FILE db2server_t.rsp
## Directory where DB2 is installed.
ENV DB2_DIR /opt/ibm/db2/V10.5
## Name of the script that downloads DB2.
ENV DB2_DOWNLOAD download

# Updates Linux. Includes i386
RUN dpkg --add-architecture i386 && \
  apt-get update && \
  apt-get install -y \
    aria2 \
    curl \
    libaio1 \
    libpam-ldap:i386 \
    libstdc++6-4.4-pic \
    lib32stdc++6

# Copies the script to downalod
COPY ${DB2_DOWNLOAD} /tmp/${DB2_DOWNLOAD}

# Download the installer.
## URL to download the installer. The link is obtained from an article in the Wiki
## https://github.com/angoca/db2-docker/wiki/db2-link-server_t
## That article should contain a valid link as the last line.
## If the link is not valid, you can modify the wiki.
RUN /tmp/download

# Extract the installer and delete the tar file.
RUN cd /tmp && \
  tar -zvxf ${DB2_INSTALLER} && \
  rm ${DB2_INSTALLER}

# Copies the response file
COPY ${DB2_RESP_FILE} /tmp/${DB2_RESP_FILE}

# Install DB2 and remove the installer.
RUN cd /tmp/${DB2_INST_DIR} && \
  ./db2prereqcheck -v ${DB2_VERSION} && \
  ( ./db2setup -r /tmp/${DB2_RESP_FILE} && \
  cat /tmp/db2setup.log || cat /tmp/db2setup.log ) && \
  ${DB2_DIR}/bin/db2val -o && \
  cd && \
  rm -Rf /tmp/${DB2_INST_DIR} && \
  rm /tmp/${DB2_RESP_FILE}

# Removes the cache of apt-get and the unnecessary packages.
RUN apt-get purge -y aria2 curl && \
  apt-get clean -y

