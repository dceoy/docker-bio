FROM centos:6

ADD https://raw.githubusercontent.com/dceoy/print-github-tags/master/print-github-tags /usr/local/bin/print-github-tags

RUN set -e \
      && yum -y upgrade \
      && yum clean all \
      && rm -rf /var/cache/yum /tmp/bcl2fastq.rpm

RUN set -eo pipefail \
      && chmod +x /usr/local/bin/print-github-tags \
      && print-github-tags --latest Illumina/manta \
        | tr -d v \
        | xargs -i curl -SL \
          https://github.com/Illumina/manta/releases/download/v{}/manta-{}.centos6_x86_64.tar.bz2 \
          -o /tmp/manta.tar.bz2 \
      && tar xvf /tmp/manta.tar.bz2 -C /usr/local/src --remove-files \
      && mv /usr/local/src/manta-* /usr/local/src/manta \
      && find /usr/local/src/manta -maxdepth 2 -type f -executable \
        -exec ln -s {} /usr/local/bin \;

ENV PYTHONPATH /usr/local/src/manta/lib/python

ENTRYPOINT ["/usr/local/bin/configManta.py"]
