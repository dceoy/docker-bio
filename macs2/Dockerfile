FROM python:2

RUN set -e \
      && apt-get -y update \
      && apt-get -y upgrade \
      && apt-get -y autoremove \
      && apt-get clean

RUN set -e \
      && pip install -U --no-cache-dir pip numpy \
      && pip install -U --no-cache-dir macs2

ENTRYPOINT ["macs2"]
