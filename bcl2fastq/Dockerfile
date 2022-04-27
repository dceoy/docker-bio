FROM centos:8

ADD bcl2fastq2-v2.20.0.422-Linux-x86_64.rpm /tmp/bcl2fastq.rpm

RUN set -e \
      && dnf -y upgrade \
      && dnf -y install /tmp/bcl2fastq.rpm \
      && dnf -y autoremove \
      && dnf clean all \
      && rm -rf /var/cache/dnf /tmp/bcl2fastq.rpm

ENTRYPOINT ["/usr/local/bin/bcl2fastq"]
