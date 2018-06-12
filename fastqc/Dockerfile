FROM ubuntu:latest

ENV DEBIAN_FRONTEND noninteractive

RUN set -e \
      && apt-get -y update \
      && apt-get -y dist-upgrade \
      && apt-get -y install curl default-jre perl unzip wget \
      && apt-get -y autoremove \
      && apt-get clean

RUN set -e \
      && curl -sS https://github.com/s-andrews/FastQC/releases/latest \
        | sed -e 's/^.*"https:\/\/github.com\/[^\/]\+\/[^\/]\+\/releases\/tag\/\([^"]\+\)".*$/\1/' \
        | xargs -i wget -L http://www.bioinformatics.babraham.ac.uk/projects/fastqc/fastqc_{}.zip -O /tmp/fastqc.zip \
      && unzip -d /usr/local/src /tmp/fastqc.zip \
      && chmod +x /usr/local/src/FastQC/fastqc \
      && ln -s /usr/local/src/FastQC/fastqc /usr/local/bin/fastqc \
      && rm -f /tmp/fastqc.zip

ENTRYPOINT ["/usr/local/bin/fastqc"]
