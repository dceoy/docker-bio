FROM ubuntu:latest

ENV DEBIAN_FRONTEND noninteractive

RUN set -e \
      && apt-get -y update \
      && apt-get -y dist-upgrade \
      && apt-get -y install curl git wget \
      && apt-get -y autoremove \
      && apt-get clean

RUN set -e \
      && git clone --bare --depth 1 https://github.com/ncbi/sra-tools.git /tmp/sra-tools.git \
      && git --git-dir=/tmp/sra-tools.git describe --tags \
        | xargs -i wget -L https://ftp-trace.ncbi.nlm.nih.gov/sra/sdk/{}/sratoolkit.{}-ubuntu64.tar.gz -O /tmp/sratoolkit.tar.gz \
      && tar xvf /tmp/sratoolkit.tar.gz -C /usr/local/src --remove-files \
      && mv /usr/local/src/sratoolkit.* /usr/local/src/sratoolkit \
      && find /usr/local/src/sratoolkit/bin -type l -maxdepth 1 | xargs -i ln -s {} /usr/local/bin \
      && rm -rf /tmp/sra-tools.git

ENTRYPOINT ["/usr/local/bin/fastq-dump"]
