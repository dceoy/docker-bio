FROM python

RUN set -e \
      && apt-get -y update \
      && apt-get -y upgrade \
      && apt-get clean

RUN set -e \
      && pip install -U pip \
      && pip install -U cutadapt

ENTRYPOINT ["cutadapt"]
