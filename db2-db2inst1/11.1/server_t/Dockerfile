# This Docker creates a db2instance
#
# Version: 2018-01-28
# Author: Andres Gomez Casanova (AngocA)
# Made in COLOMBIA.

FROM angoca/db2-instance:ese-11.1

LABEL maintainer="angoca@yahoo.com" 

# Set of variables to define the type of DB2 being installed.

## Script to create the instance
ENV DB2_INST_CREA_SCR=createInstance \
## Directory for all scripts.
    DB2_CONF=/tmp/db2_conf \
## Port number for Db2
    PORT=50000 \
## Default instance name
    DEFAULT_INSTANCE_NAME=db2inst1

WORKDIR ${DB2_CONF}

ARG INSTANCE_NAME=${DEFAULT_INSTANCE_NAME}

RUN ${DB2_CONF}/${DB2_INST_CREA_SCR} ${INSTANCE_NAME}

USER ${INSTANCE_NAME}

WORKDIR /home/${INSTANCE_NAME}

EXPOSE ${PORT}

