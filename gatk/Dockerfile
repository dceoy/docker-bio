FROM ubuntu:latest

RUN set -e \
      && apt-get -y update \
      && apt-get -y dist-upgrade \
      && apt-get -y install default-jdk git python python3 r-base \
      && apt-get -y autoremove \
      && apt-get clean

RUN set -e \
      && git clone --depth 1 https://github.com/broadinstitute/gatk.git /usr/local/src/gatk \
      && cd /usr/local/src/gatk \
      && ./gradlew localJar \
      && Rscript /usr/local/src/gatk/scripts/docker/gatkbase/install_R_packages.R

ENTRYPOINT ["java", "-jar", "/usr/local/src/gatk/build/libs/gatk.jar"]
