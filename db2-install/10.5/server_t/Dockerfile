# This Docker file downloads the DB2 LUW binaries and installs them in the
# image. It installs the necessary libraries.
#
# This Docker is designed to download a fixpack from IBM and to install DB2
# from it. The fixpack is from the server binaries that correspond to the
# Enterprise Server Edition for 90 days if a license is not applied.
#
# Version: 2018-01-28
# Author: Andres Gomez Casanova (AngocA)
# Made in COLOMBIA.

FROM ubuntu:14.04

MAINTAINER Andres Gomez <angoca@yahoo.com>

# Set of variables to define the type of DB2 being installed.

## Version of the downloaded file.
ENV DB2_VERSION=10.5 \
## Fixpack of the downloaded file.
    DB2_FIXPACK=8 \
## Directory of the installers. Associated to the edition.
    DB2_INST_DIR=server_t \
## Name of the response file included in the Docker image.
    DB2_RESP_FILE_INSTALL=db2server_t_install.rsp \
## Name of the script that downloads DB2.
    DB2_DOWNLOAD=download \
## Name of the response file included in the Docker image.
    DB2_RESP_FILE_INSTANCE=db2server_t_instance.rsp \
## Script to create the instance
    DB2_INST_CREA_SCR=createInstance \
## Directory for all scripts.
    DB2_CONF=/tmp/db2_conf

## Name of the downloaded file.
ENV DB2_INSTALLER=v${DB2_VERSION}fp${DB2_FIXPACK}_linuxx64_${DB2_INST_DIR}.tar.gz \
## Directory where DB2 is installed.
    DB2_DIR=/opt/ibm/db2/V${DB2_VERSION}

# Copies the script to download
COPY ${DB2_DOWNLOAD} /tmp/${DB2_DOWNLOAD}

# Copies the response file
COPY ${DB2_RESP_FILE_INSTALL} /tmp/${DB2_RESP_FILE_INSTALL}

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
    lib32stdc++6 && \
# Download the installer.
## URL to download the installer. The link is obtained from an article in the Wiki
## https://github.com/angoca/db2-docker/wiki/db2-link-server_t-10.5
## That article should contain a valid link as the last line.
## If the link is not valid, you can modify the wiki.
  /tmp/${DB2_DOWNLOAD} && \
# Extract the installer and delete the tar file.
  cd /tmp && \
  tar -zvxf ${DB2_INSTALLER} && \
  rm ${DB2_INSTALLER} && \
# Install DB2 and remove the installer.
  cd /tmp/${DB2_INST_DIR} && \
  ./db2prereqcheck -l && \
  ( ./db2setup -r /tmp/${DB2_RESP_FILE_INSTALL} && \
  cat /tmp/db2setup.log || cat /tmp/db2setup.log ) && \
  ${DB2_DIR}/bin/db2val -o && \
  cd && \
  rm -Rf /tmp/${DB2_INST_DIR} && \
  rm /tmp/${DB2_RESP_FILE_INSTALL} && \
# Removes the cache of apt-get and the unnecessary packages.
  apt-get purge -y aria2 curl && \
  apt-get clean -y && \
# Removes the list of packages
  rm -rf /var/lib/apt/lists/*

RUN env
# Creates a directory for all scripts
WORKDIR ${DB2_CONF}

# Copies the response file
COPY ${DB2_RESP_FILE_INSTANCE} ${DB2_CONF}/${DB2_RESP_FILE_INSTANCE}

# Copies the script to create the instance
COPY ${DB2_INST_CREA_SCR} ${DB2_CONF}/${DB2_INST_CREA_SCR}

