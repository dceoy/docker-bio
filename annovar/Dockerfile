FROM ubuntu:latest

ADD annovar.latest.tar.gz /tmp/annovar.latest.tar.gz

RUN set -e \
      && apt-get -y update \
      && apt-get -y dist-upgrade \
      && apt-get -y install --no-install-recommends --no-install-suggests perl \
      && apt-get -y autoremove \
      && apt-get clean \
      && rm -rf /var/lib/apt/lists/*

RUN set -e \
      && tar xvf /tmp/annovar.latest.tar.gz -C /usr/local/src --remove-files \
      && find /usr/local/src/annovar -type f -maxdepth 1 -executable \
        | xargs -i ln -s {} /usr/local/bin

ENTRYPOINT ["/usr/bin/perl", "/usr/local/src/annovar/annotate_variation.pl"]
