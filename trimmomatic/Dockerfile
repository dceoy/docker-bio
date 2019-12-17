FROM ubuntu:latest

ENV DEBIAN_FRONTEND noninteractive

ADD https://github.com/timflutre/trimmomatic/archive/master.tar.gz /tmp/trimmomatic.tar.gz

RUN set -e \
      && ln -sf /bin/bash /bin/sh

RUN set -e \
      && apt-get -y update \
      && apt-get -y dist-upgrade \
      && apt-get -y install --no-install-recommends --no-install-suggests \
        default-jdk make \
      && apt-get -y autoremove \
      && apt-get clean \
      && rm -rf /var/lib/apt/lists/*

RUN set -e \
      && tar xvf /tmp/trimmomatic.tar.gz -C /usr/local/src --remove-files \
      && mv /usr/local/src/trimmomatic-* /usr/local/src/trimmomatic \
      && cd /usr/local/src/trimmomatic \
      && make

ENTRYPOINT ["/usr/bin/java", "-jar", "/usr/local/src/trimmomatic/classes/trimmomatic.jar"]
