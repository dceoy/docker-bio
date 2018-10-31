FROM ubuntu:latest

ADD https://bootstrap.pypa.io/get-pip.py /tmp/get-pip.py

RUN set -e \
      && apt-get -y update \
      && apt-get -y dist-upgrade \
      && apt-get -y install --no-install-recommends --no-install-suggests \
        ca-certificates curl gcc g++ libcurl4-gnutls-dev libz-dev python-dev \
      && apt-get -y autoremove \
      && apt-get clean \
      && rm -rf /var/lib/apt/lists/*


RUN set -e \
      && /usr/bin/python /tmp/get-pip.py \
      && pip install -U --no-cache-dir numpy pip pyvcf \
      && curl -sS https://github.com/broadinstitute/oncotator/releases/latest \
        | sed -e 's/^.*"\(https:\/\/github.com\/[^\/]\+\/[^\/]\+\/\)releases\/tag\(\/[^"]\+\)".*$/\1archive\2\.tar\.gz/' \
        | xargs -i curl -SL {} -o /tmp/oncotator.tar.gz \
      && tar xvf /tmp/oncotator.tar.gz -C /tmp --remove-files \
      && cd /tmp/oncotator-* \
      && /usr/bin/python setup.py install \
      && rm -rf /tmp/get-pip.py /tmp/oncotator-*

ENTRYPOINT ["/usr/local/bin/Oncotator"]
