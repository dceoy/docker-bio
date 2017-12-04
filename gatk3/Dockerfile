FROM ubuntu

ADD https://github.com/broadgsa/gatk-protected/archive/master.tar.gz /tmp/gatk.tar.gz

RUN set -e \
      && apt-get -y update \
      && apt-get -y install maven software-properties-common \
      && add-apt-repository ppa:webupd8team/java \
      && apt-get -y update \
      && apt-get -y upgrade \
      && yes yes | apt-get -y install oracle-java8-installer \
      && apt-get -y autoremove \
      && apt-get clean

RUN set -e \
      && tar xvf /tmp/gatk.tar.gz -C /usr/local/src \
      && mv /usr/local/src/gatk-protected-master /usr/local/src/gatk \
      && cd /usr/local/src/gatk \
      && mvn package \
      && rm -rf /tmp/*

ENTRYPOINT ["java", "-jar", "/usr/local/src/gatk/target/GenomeAnalysisTK.jar"]
