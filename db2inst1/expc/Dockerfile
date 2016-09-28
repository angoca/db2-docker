# This Docker creates a db2instance
#
# Version: 2016-09-28
# Author: Andres Gomez Casanova (AngocA)
# Made in COLOMBIA.

FROM angoca/db2-instance:expc

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

## Script to create the instance
ENV DB2_INST_CREA_SCR createInstance
## Directory for all scripts.
ENV DB2_CONF /tmp/db2_conf

WORKDIR /tmp/db2_conf

RUN /tmp/db2_conf/${DB2_INST_CREA_SCR}

EXPOSE 50000

USER db2inst1

WORKDIR /home/db2inst1

#ENTRYPOINT ["db2"]
#CMD ["?"]

