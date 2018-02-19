FROM ubuntu

ADD ftp://ftp.ccb.jhu.edu/pub/infphilo/hisat2/downloads/hisat2-2.1.0-Linux_x86_64.zip /tmp/hisat2.zip

RUN set -e \
      && apt-get -y update \
      && apt-get -y upgrade \
      && apt-get -y install unzip \
      && apt-get -y autoremove \
      && apt-get clean

RUN set -e \
      && unzip -d /usr/local/src /tmp/hisat2.zip \
      && mv /usr/local/src/hisat2-* /usr/local/src/hisat2 \
      && find /usr/local/src/hisat2 -type f -maxdepth 1 -executable | xargs -i ln -s {} /usr/local/bin \
      && rm -rf /tmp/*

ENTRYPOINT ["hisat2"]
