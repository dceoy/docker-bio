FROM centos

ADD http://jp.support.illumina.com/content/dam/illumina-support/documents/downloads/software/bcl2fastq/bcl2fastq2-v2-20-0-linux-x86-64.zip /tmp/bcl2fastq.zip

RUN set -e \
      && yum -y upgrade \
      && yum -y install unzip \
      && unzip /tmp/bcl2fastq.zip -d /tmp \
      && yum -y install /tmp/bcl2fastq2-*.rpm \
      && yum clean all \
      && rm -rf /tmp/*

ENTRYPOINT ["bcl2fastq"]
