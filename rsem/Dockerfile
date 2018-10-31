FROM ubuntu:latest

ENV DEBIAN_FRONTEND noninteractive

RUN set -e \
      && apt-get -y update \
      && apt-get -y dist-upgrade \
      && apt-get -y install --no-install-recommends --no-install-suggests \
        ca-certificates curl g++ gcc libtbb-dev libz-dev make perl perl-doc \
      && apt-get -y autoremove \
      && apt-get clean \
      && rm -rf /var/lib/apt/lists/*

RUN set -e \
      && curl -sS https://github.com/BenLangmead/bowtie2/releases/latest \
        | sed -e 's/^.*"\(https:\/\/github.com\/[^\/]\+\/[^\/]\+\/\)releases\/tag\(\/[^"]\+\)".*$/\1archive\2\.tar\.gz/' \
        | xargs -i curl -SL {} -o /tmp/bowtie2.tar.gz \
      && tar xvf /tmp/bowtie2.tar.gz -C /usr/local/src --remove-files \
      && mv /usr/local/src/bowtie2-* /usr/local/src/bowtie2 \
      && cd /usr/local/src/bowtie2 \
      && make \
      && make install

RUN set -e \
      && curl -sS https://github.com/alexdobin/STAR/releases/latest \
        | sed -e 's/^.*"\(https:\/\/github.com\/[^\/]\+\/[^\/]\+\/\)releases\/tag\(\/[^"]\+\)".*$/\1archive\2\.tar\.gz/' \
        | xargs -i curl -SL {} -o /tmp/star.tar.gz \
      && tar xvf /tmp/star.tar.gz -C /usr/local/src --remove-files \
      && mv /usr/local/src/STAR-* /usr/local/src/STAR \
      && cd /usr/local/src/STAR/source \
      && make STAR \
      && ln -s /usr/local/src/STAR/source/STAR /usr/local/bin/STAR

RUN set -e \
      && curl -sS https://github.com/deweylab/RSEM/releases/latest \
        | sed -e 's/^.*"\(https:\/\/github.com\/[^\/]\+\/[^\/]\+\/\)releases\/tag\(\/[^"]\+\)".*$/\1archive\2\.tar\.gz/' \
        | xargs -i curl -SL {} -o /tmp/rsem.tar.gz \
      && tar xvf /tmp/rsem.tar.gz -C /usr/local/src --remove-files \
      && mv /usr/local/src/RSEM-* /usr/local/src/RSEM \
      && cd /usr/local/src/RSEM \
      && make \
      && make install

ENTRYPOINT ["/usr/local/bin/rsem-calculate-expression"]
