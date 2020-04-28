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
      && tar xvf /tmp/trimmomatic.tar.gz -C /opt --remove-files \
      && mv /opt/trimmomatic-* /opt/trimmomatic \
      && cd /opt/trimmomatic \
      && make

RUN set -e \
      && mkdir /opt/trimmomatic/bin \
      && echo '#!/usr/bin/env bash' > /opt/trimmomatic/bin/trimmomatic \
      && echo 'java -jar /opt/trimmomatic/classes/trimmomatic.jar ${@}' \
        >> /opt/trimmomatic/bin/trimmomatic \
      && chmod +x /opt/trimmomatic/bin/trimmomatic

ENV PATH /opt/trimmomatic/bin:${PATH}

ENTRYPOINT ["/usr/bin/java", "-jar", "/opt/trimmomatic/classes/trimmomatic.jar"]
