# This Docker file downloads the DB2 LUW binaries and installs them in the
# image. It installs the necessary libraries.
#
# This Docker is designed to download the DB2 free edition from IBM and to
# install DB2 from it. This edition does not requieres a license.
#
# Version: 2018-01-25
# Author: Andres Gomez Casanova (AngocA)
# Made in COLOMBIA.

FROM ubuntu:14.04

MAINTAINER Andres Gomez <angoca@yahoo.com>

# MicroBadge
ARG VCS_REF

LABEL org.label-schema.build-date=${BUILD_DATE} \
      org.label-schema.name="db2-docker" \
      org.label-schema.description="Docker container for IBM DB2 for LUW" \
      org.label-schema.url="https://github.com/angoca/db2-docker/wiki" \
      org.label-schema.vcs-ref=$VCS_REF \
      org.label-schema.vcs-url="https://github.com/angoca/db2-docker" \
      org.label-schema.vendor="AngocA" \
      org.label-schema.version="1.0-11.1-instance-expc" \
      org.label-schema.schema-version="1.0"

# Set of variables to define the type of DB2 being installed.

## Version of the downloaded file.
ENV DB2_VERSION 11.1
## Fixpack of the downloaded file.
ENV DB2_FIXPACK GA
## Name of the downloaded file.
ENV DB2_INSTALLER v${DB2_VERSION}_linuxx64_expc.tar.gz
## Directory of the installers. Associated to the edition.
ENV DB2_INST_DIR expc
## Name of the response file included in the Docker image.
ENV DB2_RESP_FILE db2expc.rsp
## Directory where DB2 is installed.
ENV DB2_DIR /opt/ibm/db2/V${DB2_VERSION}
## Name of the script that downloads DB2.
ENV DB2_DOWNLOAD download

# Copies the script to download
COPY ${DB2_DOWNLOAD} /tmp/${DB2_DOWNLOAD}

# Copies the response file
COPY ${DB2_RESP_FILE} /tmp/${DB2_RESP_FILE}

# Run all commands in a single RUN layer to minimize the size of the image.
# Updates Linux. Includes i386
RUN dpkg --add-architecture i386 && \
  apt-get update && \
  apt-get install -y \
    aria2 \
    curl \
    libaio1 \
    libpam-ldap:i386 \
    libstdc++6-4.4-pic \
    numactl \
    lib32stdc++6 && \
    rpm \
# Download the installer.
## URL to download the installer. The link is obtained from an article in the Wiki
## https://github.com/angoca/db2-docker/wiki/db2-link-expc
## That article should contain a valid link as the last line.
## If the link is not valid, you can modify the wiki.
  echo "Downloading..." && \
  /tmp/${DB2_DOWNLOAD} && \
# Extract the installer and delete the tar file.
  echo "Extracting..." && \
  cd /tmp && \
  tar -zvxf ${DB2_INSTALLER} && \
  rm ${DB2_INSTALLER} && \
# Install DB2 and remove the installer.
  echo "Checking prereqs..." && \
  cd /tmp/${DB2_INST_DIR} && \
  ./db2prereqcheck -l && \
  echo "Installing..." && \
  ( ./db2setup -r /tmp/${DB2_RESP_FILE} && \
  echo "Showing installation log..." && \
  cat /tmp/db2setup.log || cat /tmp/db2setup.log ) && \
  echo "Validating installation..." && \
  ${DB2_DIR}/bin/db2val -o && \
  cd && \
  echo "Removing files..." && \
  rm -Rf /tmp/${DB2_INST_DIR} && \
  rm /tmp/${DB2_RESP_FILE} && \
# Removes the cache of apt-get and the unnecessary packages.
  apt-get purge -y aria2 curl && \
  apt-get clean -y && \
# Removes the list of packages
  rm -rf /var/lib/apt/lists/*

