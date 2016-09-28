# This Docker file downloads the DB2 LUW binaries and install them in the image.
# It install the necessary libraries.
#
# Version: 2015-01-04
# Author: Andres Gomez Casanova (AngocA)
# Made in COLOMBIA.

FROM angoca/db2-install:expc

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

## Name of the response file included in the Docker image.
ENV DB2_RESP_FILE db2expc.rsp
## Script to create the instance
ENV DB2_INST_CREA_SCR createInstance
## Directory for all scripts.
ENV DB2_CONF /tmp/db2_conf

RUN env
# Creates a directory for all scripts
RUN mkdir ${DB2_CONF}
WORKDIR /tmp/db2_conf

# Copies the response file
COPY ${DB2_RESP_FILE} ${DB2_CONF}/${DB2_RESP_FILE}

# Copies the script to create the instance
COPY ${DB2_INST_CREA_SCR} ${DB2_CONF}/${DB2_INST_CREA_SCR}


