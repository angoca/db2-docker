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

## URL to download the installer. From IBM, but it has to be updated because the
## link is temporal. You can get a new valid link from
## http://www.ibm.com/support/fixcentral/swg/quickorder?parent=ibm%7EInformation%2BManagement&product=ibm/Information+Management/DB2&release=10.5.*&platform=Linux+64-bit,x86_64&function=fixId&fixids=DB2-linuxx64-server_t-10.5.0.5-FP005&includeRequisites=1&includeSupersedes=0&downloadMethod=http&source=fc
ENV DB2_BIN https://delivery04.dhe.ibm.com/sdfdl/v2/sar/CM/IM/04yrx/0/Xa.2/Xb.jusyLTSp44S0MSO8Z59OKiPuice1BoD2NtK-w79dUdtSfR_F1xHav7vl7fo/Xc.CM/IM/04yrx/0/v10.5fp5_linuxx64_server_t.tar.gz/Xd./Xf.LPR.D1vk/Xg.7915501/Xi.habanero/XY.habanero/XZ.64S49xR9TwcWgPsBbVY8_2teJCY/v10.5fp5_linuxx64_server_t.tar.gz
## Name of the downloaded file.
ENV DB2_INSTALLER v10.5fp5_linuxx64_server_t.tar.gz
## Directory of the installers. Associated to the edition.
ENV DB2_INST_DIR server_t
## Version of the downloaded file. Used for db2prereqcheck.
ENV DB2_VERSION 10.5.0.5
## Name of the response file included in the Docker image.
ENV DB2_RESP_FILE db2server_t.rsp

# Updates Linux. Includes i386
RUN dpkg --add-architecture i386 && \
  apt-get update && \
  apt-get install -y \
    aria2 \
    libstdc++6-4.4-pic \
    libaio1 \
    libpam-ldap:i386 \
    lib32stdc++6

# Download the installer.
RUN cd /tmp && \
  aria2c -x 16 ${DB2_BIN}

# Extract the installer and delete the tar file.
RUN cd /tmp && \
  tar -zvxf ${DB2_INSTALLER} && \
  rm ${DB2_INSTALLER}

# Copies the response file
COPY ${DB2_RESP_FILE} /tmp/${DB2_RESP_FILE}

# Install DB2 and remove the installer.
RUN cd /tmp/${DB2_INST_DIR} && \
  ./db2prereqcheck -v ${DB2_VERSION} && \
  ./db2setup -r /tmp/${DB2_RESP_FILE} && \
  cat /tmp/db2setup.log && \
  cd && \
  rm -Rf /tmp/${DB2_INST_DIR} && \
  rm /tmp/${DB2_RESP_FILE}

# Removes the cache of apt-get and the unnecessary packages.
RUN apt-get purge -y aria2 && \
  apt-get clean -y

