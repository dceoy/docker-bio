FROM python

RUN set -e \
      && apt-get -y update \
      && apt-get -y upgrade \
      && apt-get clean

RUN set -e \
      && pip install -U --no-cache-dir pip \
      && pip install -U --no-cache-dir cutadapt

ENTRYPOINT ["cutadapt"]
