FROM ubuntu:latest

ENV DEBIAN_FRONTEND noninteractive

RUN set -e \
      && apt-get -y update \
      && apt-get -y dist-upgrade \
      && apt-get -y install curl default-jre wget \
      && apt-get -y autoremove \
      && apt-get clean

RUN set -e \
      && curl -sS https://github.com/broadinstitute/picard/releases/latest \
        | sed -e 's/^.*"\(https:\/\/github.com\/[^\/]\+\/[^\/]\+\/releases\/\)tag\(\/[^"]\+\)".*$/\1download\2\/picard.jar/' \
        | xargs -i wget -L {} -O /usr/local/src/picard.jar

ENTRYPOINT ["java", "-jar", "/usr/local/src/picard.jar"]
