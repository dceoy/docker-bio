FROM ubuntu:latest

RUN set -e \
      && apt-get -y update \
      && apt-get -y dist-upgrade \
      && apt-get -y install default-jdk git \
      && apt-get -y autoremove \
      && apt-get clean

RUN set -e \
      && git clone --depth 1 https://github.com/broadinstitute/picard.git /usr/local/src/picard \
      && cd /usr/local/src/picard \
      && ./gradlew shadowJar

ENTRYPOINT ["java", "-jar", "/usr/local/src/picard/build/libs/picard.jar"]
