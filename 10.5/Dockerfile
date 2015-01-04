FROM ubuntu:last

RUN dpkg --add-architecture i386 && \
  apt-get update && \
  apt-get install -y -qq \
    aria2 \
    libaio1 \
    libpam-ldap:i386 \
    libstdc++6-4.4-pic \
    lib32stdc++6

RUN cd /tmp && \
  aria2c -x 16 https://www.dropbox.com/s/ut3136498v8lbti/v10.5_linuxx64_expc.tar.gz \
    | tar -xJC /tmp && \
  cd expc && \
  db2_install

