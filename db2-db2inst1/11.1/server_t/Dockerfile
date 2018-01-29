# This Docker creates a db2instance
#
# Version: 2018-01-28
# Author: Andres Gomez Casanova (AngocA)
# Made in COLOMBIA.

FROM angoca/db2-install:ese-11.1

LABEL maintainer="angoca@yahoo.com" 

# Set of variables to define the type of DB2 being installed.

## Script to create the instance
ENV DB2_INST_CREA_SCR=createInstance \
## Directory for all scripts.
    DB2_CONF=/tmp/db2_conf \
## Response file name
    DB2_RESP_FILE=db2server_t_instance.rsp \
## Port number for Db2
    PORT=50000 \
## Default instance name
    DEFAULT_INSTANCE_NAME=db2inst1

WORKDIR ${DB2_CONF}

ARG INSTANCE_NAME=${DEFAULT_INSTANCE_NAME}

RUN ${DB2_CONF}/${DB2_INST_CREA_SCR} ${INSTANCE_NAME} && \
# Modifies the db2nodes file to include a valid name.
  cat /home/${INSTANCE_NAME}/sqllib/db2nodes.cfg && \
  echo "0 localhost 0" > /home/${INSTANCE_NAME}/sqllib/db2nodes.cfg && \
  cat /home/${INSTANCE_NAME}/sqllib/db2nodes.cfg

USER ${INSTANCE_NAME}

WORKDIR /home/${INSTANCE_NAME}

EXPOSE ${PORT}

