FROM ubuntu:latest

RUN set -e \
      && apt-get -y update \
      && apt-get -y upgrade \
      && apt-get -y install default-jre git \
      && apt-get -y autoremove \
      && apt-get clean

RUN set -e \
      && git clone --depth 1 https://github.com/dkoboldt/varscan.git /usr/local/src/varscan

ENTRYPOINT ["java", "-jar", "/usr/local/src/picard/VarScan.v2.4.0.jar"]
