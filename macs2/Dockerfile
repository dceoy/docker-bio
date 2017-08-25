FROM python:2

RUN set -e \
      && apt-get -y update \
      && apt-get -y upgrade \
      && apt-get clean

RUN set -e \
      && pip install -U pip numpy \
      && pip install -U macs2

ENTRYPOINT ["macs2"]
