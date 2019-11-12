FROM ubuntu:latest

ENV DEBIAN_FRONTEND noninteractive

ADD https://bootstrap.pypa.io/get-pip.py /tmp/get-pip.py
ADD https://raw.githubusercontent.com/dceoy/print-github-tags/master/print-github-tags /usr/local/bin/print-github-tags

RUN set -e \
      && apt-get -y update \
      && apt-get -y dist-upgrade \
      && apt-get -y install --no-install-recommends --no-install-suggests \
        ca-certificates curl gcc make python-dev \
      && apt-get -y autoremove \
      && apt-get clean \
      && rm -rf /var/lib/apt/lists/*

RUN set -e \
      && chmod +x /usr/local/bin/print-github-tags \
      && print-github-tags --release --latest --tar root-project/root \
        | xargs -i curl -SL {} -o /tmp/root.tar.gz \
      && tar xvf /tmp/root.tar.gz -C /usr/local/src --remove-files \
      && mv /usr/local/src/root-* /usr/local/src/root \
      && cd /usr/local/src/root \
      && ./configure \
      && make \
      && find /usr/local/src/root -maxdepth 1 -type f -executable \
        -exec ln -s {} /usr/local/bin \;

RUN set -e \
      && print-github-tags --release --latest --tar hall-lab/speedseq \
        | xargs -i curl -SL {} -o /tmp/speedseq.tar.gz \
      && tar xvf /tmp/speedseq.tar.gz -C /usr/local/src --remove-files \
      && mv /usr/local/src/speedseq-* /usr/local/src/speedseq \
      && source /usr/local/src/root/bin/thisroot.sh \
      && cd /usr/local/src/speedseq \
      && make cnvnator \
      && find /usr/local/src/speedseq -maxdepth 1 -type f -executable \
        -exec ln -s {} /usr/local/bin \;

RUN set -e \
      && /usr/bin/python /tmp/get-pip.py \
      && pip install -U --no-cache-dir pip numpy \
      && pip install -U --no-cache-dir svtools \
      && rm -f /tmp/get-pip.py

ENTRYPOINT ["/usr/local/bin/svtools"]
