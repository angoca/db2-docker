# This Docker file downloads the DB2 LUW binaries and install them in the image.
# It install the necessary libraries.
#
# Version: 2015-01-04
# Author: Andres Gomez Casanova (AngocA)
# Made in COLOMBIA.

FROM angoca/db2-install:ese

MAINTAINER Andres Gomez <angoca@yahoo.com>

# Set of variables to define the type of DB2 being installed.

## Name of the response file included in the Docker image.
ENV DB2_RESP_FILE db2server_t.rsp

# Copies the response file
COPY ${DB2_RESP_FILE} /tmp/${DB2_RESP_FILE}

# Creates the instance with the provided response file.
RUN ${DB2_DIR}/instance/db2isetup -r /tmp/${DB2_RESP_FILE} || \
  cat /tmp/db2isetup.log && \
  rm /tmp/${DB2_RESP_FILE}

EXPOSE 50000

USER db2inst1

WORKDIR /home/db2inst1

#ENTRYPOINT ["db2"]
#CMD ["?"]


