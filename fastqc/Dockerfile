FROM java:jre

ADD http://www.bioinformatics.babraham.ac.uk/projects/fastqc/fastqc_v0.11.5.zip /tmp/fastqc.zip

RUN set -e \
      && apt-get -y update \
      && apt-get -y upgrade \
      && apt-get -y install unzip perl \
      && apt-get clean

RUN set -e \
      && unzip -d /usr/local/src /tmp/fastqc.zip \
      && chmod +x /usr/local/src/FastQC/fastqc \
      && ln -s /usr/local/src/FastQC/fastqc /usr/local/bin/fastqc \
      && rm -rf /tmp/*

ENTRYPOINT ["fastqc"]
