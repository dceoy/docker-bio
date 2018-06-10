FROM ubuntu:latest

ENV DEBIAN_FRONTEND noninteractive

ADD https://ftp-trace.ncbi.nlm.nih.gov/sra/sdk/2.8.2-1/sratoolkit.2.8.2-1-ubuntu64.tar.gz /tmp/sratoolkit.tar.gz

RUN set -e \
      && apt-get -y update \
      && apt-get -y dist-upgrade \
      && apt-get -y autoremove \
      && apt-get clean

RUN set -e \
      && tar xvf /tmp/sratoolkit.tar.gz -C /usr/local/src --remove-files \
      && mv /usr/local/src/sratoolkit.* /usr/local/src/sratoolkit \
      && find /usr/local/src/sratoolkit/bin -type l -maxdepth 1 | xargs -i ln -s {} /usr/local/bin

ENTRYPOINT ["fastq-dump"]
