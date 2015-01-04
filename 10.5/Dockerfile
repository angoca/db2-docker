FROM ubuntu:14.04
MAINTAINER Andres Gomez <angoca@yahoo.com>

#RUN dpkg --add-architecture i386 && \
RUN apt-get update && \
  apt-get install -y -qq \
    aria2 
    #libaio1 \
    #libpam-ldap:i386 \
    #libstdc++6-4.4-pic \
    #lib32stdc++6

# Download the installer.
RUN cd /tmp && \
  aria2c -x 16 https://iwm.dhe.ibm.com/sdfdl/v2/regs2/db2pmopn/db2_v105/expc/Xa.2/Xb.aA_60_-i75MwL9JKb3_JnLkeDltZUdcgF5mlWmBo_g/Xc.db2_v105/expc/v10.5_linuxx64_expc.tar.gz/Xd./Xf.LPr.D1vk/Xg.7896296/Xi.swg-db2expressc/XY.regsrvs/XZ.USh1SRvgyXVOj1uqGuKpSQk2Sqg/v10.5_linuxx64_expc.tar.gz

# Extract the installer and delete the tar file.
RUN cd /tmp && \
  tar -zvxf v10.5_linuxx64_expc.tar.gz && \
  rm v10.5_linuxx64_expc.tar.gz

# Install DB2 and remove the installer.
RUN cd /tmp/expc && \
  sudo ./db2_install && \
  cd && \
  rm -Rf /tmp/expc


