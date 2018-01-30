# This Docker creates a db2instance
#
# Version: 2016-05-16
# Author: Andres Gomez Casanova (AngocA)
# Made in COLOMBIA.

FROM angoca/db2-install:ese-10.5

MAINTAINER Andres Gomez <angoca@yahoo.com>

# Set of variables to define the type of DB2 being installed.

## Script to create the instance
ENV DB2_INST_CREA_SCR=createInstance \
## Directory for all scripts.
    DB2_CONF=/tmp/db2_conf  \
## Response file name
    DB2_RESP_FILE=db2server_t_instance.rsp \
## Default instance name
    INSTANCE_NAME=db2inst1

WORKDIR /tmp/db2_conf

RUN /tmp/db2_conf/${DB2_INST_CREA_SCR} && \
# Modifies the db2nodes file to include a valid name.
  cat /home/${INSTANCE_NAME}/sqllib/db2nodes.cfg && \
  echo "0 localhost 0" > /home/${INSTANCE_NAME}/sqllib/db2nodes.cfg && \
  cat /home/${INSTANCE_NAME}/sqllib/db2nodes.cfg

EXPOSE 50000

USER db2inst1

WORKDIR /home/db2inst1

