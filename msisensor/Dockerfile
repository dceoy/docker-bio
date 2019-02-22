FROM ubuntu:latest

ENV DEBIAN_FRONTEND noninteractive

ADD https://raw.githubusercontent.com/dceoy/print-github-tags/master/print-github-tags /usr/local/bin/print-github-tags

RUN set -e \
      && apt-get -y update \
      && apt-get -y dist-upgrade \
      && apt-get -y install --no-install-recommends --no-install-suggests \
        ca-certificates curl g++ gcc libncurses5-dev libncursesw5-dev make \
        zlib1g-dev \
      && apt-get -y autoremove \
      && apt-get clean \
      && rm -rf /var/lib/apt/lists/*

RUN set -e \
      && chmod +x /usr/local/bin/print-github-tags \
      && print-github-tags --latest --tar ding-lab/msisensor \
        | xargs -i curl -SL {} -o /tmp/msisensor.tar.gz \
      && tar xvf /tmp/msisensor.tar.gz -C /usr/local/src --remove-files \
      && mv /usr/local/src/msisensor-* /usr/local/src/msisensor \
      && cd /usr/local/src/msisensor \
      && make \
      && find /usr/local/src/msisensor -type f -maxdepth 1 -executable \
        | xargs -i ln -s {} /usr/local/bin

ENTRYPOINT ["/usr/local/bin/msisensor"]
