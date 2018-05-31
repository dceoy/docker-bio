FROM python:2

RUN set -e \
      && apt-get -y update \
      && apt-get -y dist-upgrade \
      && apt-get -y autoremove \
      && apt-get clean

RUN set -e \
      && git clone --depth 1 https://github.com/broadinstitute/oncotator.git /tmp/oncotator \
      && pip install -U --no-cache-dir numpy pyvcf \
      && cd /tmp/oncotator \
      && python setup.py install \
      && rm -rf /tmp/oncotator

ENTRYPOINT ["Oncotator"]
