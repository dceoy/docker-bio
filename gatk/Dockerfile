FROM maven

ADD https://github.com/broadgsa/gatk-protected/archive/master.tar.gz /tmp/gatk.tar.gz

RUN set -e \
      && apt-get -y update \
      && apt-get -y upgrade \
      && apt-get clean

RUN set -e \
      && tar xvf /tmp/gatk.tar.gz -C /usr/local/src \
      && mv /usr/local/src/gatk-protected-master /usr/local/src/gatk \
      && cd /usr/local/src/gatk \
      && mvn package \
      && rm -rf /tmp/*

ENTRYPOINT ["java", "-jar", "/usr/local/src/gatk-protected/target/GenomeAnalysisTK.jar"]
