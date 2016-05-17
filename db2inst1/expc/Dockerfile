# This Docker creates a db2instance
#
# Version: 2016-05-16
# Author: Andres Gomez Casanova (AngocA)
# Made in COLOMBIA.

FROM angoca/db2-instance:expc

MAINTAINER Andres Gomez <angoca@yahoo.com>

# Set of variables to define the type of DB2 being installed.

## Script to create the instance
ENV DB2_INST_CREA_SCR createInstance
## Directory for all scripts.
ENV DB2_CONF /tmp/db2_conf

WORKDIR /tmp/db2_conf

EXEC /tmp/db2_conf/${DB2_INST_CREA_SCR}

EXPOSE 50000

USER db2inst1

WORKDIR /home/db2inst1

#ENTRYPOINT ["db2"]
#CMD ["?"]


