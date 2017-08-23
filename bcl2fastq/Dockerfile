FROM centos

ADD https://support.illumina.com/content/dam/illumina-support/documents/downloads/software/bcl2fastq/bcl2fastq2-v2.19.0.316-Linux-x86_64.rpm /tmp/bcl2fastq2.rpm

RUN set -e \
      && yum -y upgrade \
      && yum -y install /tmp/bcl2fastq2.rpm \
      && yum clean all \
      && rm -rf /tmp/*

ENTRYPOINT ["bcl2fastq"]
