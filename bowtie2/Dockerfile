FROM gcc

ADD https://github.com/BenLangmead/bowtie2/releases/download/v2.3.2/bowtie2-2.3.2-linux-x86_64.zip /tmp/bowtie2.zip

RUN set -e \
      && apt-get -y update \
      && apt-get -y install unzip \
      && apt-get clean

RUN set -e \
      && unzip -d /usr/local/src /tmp/bowtie2.zip \
      && mv /usr/local/src/bowtie2-* /usr/local/src/bowtie2 \
      && find /usr/local/src/bowtie2 -type f -maxdepth 1 -executable | xargs -i ln -s {} /usr/local/bin \
      && rm -rf /tmp/*

ENTRYPOINT ["bowtie2"]
