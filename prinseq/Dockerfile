FROM perl:latest

ADD https://sourceforge.net/projects/prinseq/files/latest/download?source=files /tmp/prinseq.tar.gz

RUN set -e \
      && apt-get -y update \
      && apt-get -y dist-upgrade \
      && apt-get -y autoremove \
      && apt-get clean

RUN set -e \
      && tar xvf /tmp/prinseq.tar.gz -C /usr/local/src --remove-files \
      && mv /usr/local/src/prinseq-* /usr/local/src/prinseq \
      && chmod +x /usr/local/src/prinseq/*.pl \
      && find /usr/local/src/prinseq -type f -maxdepth 1 -executable | xargs -i ln -s {} /usr/local/bin

ENTRYPOINT ["/usr/local/bin/perl", "/usr/local/src/prinseq/prinseq-lite.pl"]
