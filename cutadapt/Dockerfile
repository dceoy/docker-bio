FROM python:latest

RUN set -e \
      && apt-get -y update \
      && apt-get -y upgrade \
      && apt-get -y autoremove \
      && apt-get clean

RUN set -e \
      && pip install -U --no-cache-dir pip cutadapt

ENTRYPOINT ["cutadapt"]
