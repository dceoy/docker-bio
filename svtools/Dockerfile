FROM ubuntu:latest

ENV DEBIAN_FRONTEND noninteractive

ADD https://bootstrap.pypa.io/get-pip.py /tmp/get-pip.py
ADD https://raw.githubusercontent.com/dceoy/print-github-tags/master/print-github-tags /usr/local/bin/print-github-tags

RUN set -e \
      && apt-get -y update \
      && apt-get -y dist-upgrade \
      && apt-get -y install --no-install-recommends --no-install-suggests \
        ca-certificates curl gcc libbz2-dev libcurl4-gnutls-dev liblzma-dev \
        libncurses5-dev libssl-dev libz-dev python-dev zlib1g-dev \
      && apt-get -y autoremove \
      && apt-get clean \
      && rm -rf /var/lib/apt/lists/*

RUN set -e \
      && chmod +x /usr/local/bin/print-github-tags \
      && print-github-tags --release --latest --tar ebiggers/libdeflate \
        | xargs -i curl -SL {} -o /tmp/libdeflate.tar.gz \
      && tar xvf /tmp/libdeflate.tar.gz -C /usr/local/src --remove-files \
      && mv /usr/local/src/libdeflate-* /usr/local/src/libdeflate \
      && make

ENV LD_LIBRARY_PATH /usr/local/src/libdeflate

RUN set -e \
      && /usr/bin/python /tmp/get-pip.py \
      && pip install -U --no-cache-dir pip numpy \
      && pip install -U --no-cache-dir svtools \
      && rm -f /tmp/get-pip.py

ENTRYPOINT ["/usr/local/bin/svtools"]
