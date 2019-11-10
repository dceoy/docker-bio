FROM centos:7

ADD bcl2fastq2-v2.20.0.422-Linux-x86_64.rpm /tmp/bcl2fastq.rpm

RUN set -e \
      && yum -y upgrade \
      && yum -y install /tmp/bcl2fastq.rpm \
      && yum -y autoremove \
      && yum clean all \
      && rm -rf /var/cache/yum /tmp/bcl2fastq.rpm

ENTRYPOINT ["/usr/local/bin/bcl2fastq"]
