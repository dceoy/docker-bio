FROM ubuntu

ADD https://ftp-trace.ncbi.nlm.nih.gov/sra/sdk/2.8.2-1/sratoolkit.2.8.2-1-ubuntu64.tar.gz /tmp/sratoolkit.tar.gz

RUN set -e \
      && tar xvf /tmp/sratoolkit.tar.gz -C /usr/local/src \
      && mv /usr/local/src/sratoolkit.* /usr/local/src/sratoolkit \
      && find /usr/local/src/sratoolkit/bin -type l -maxdepth 1 | xargs -i ln -s {} /usr/local/bin

ENTRYPOINT ["fastq-dump"]
