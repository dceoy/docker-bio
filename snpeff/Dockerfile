FROM ubuntu:latest

ENV DEBIAN_FRONTEND noninteractive

RUN set -e \
      && ln -sf bash /bin/sh

RUN set -e \
      && apt-get -y update \
      && apt-get -y dist-upgrade \
      && apt-get -y install --no-install-recommends --no-install-suggests \
        ca-certificates curl openjdk-8-jre unzip \
      && apt-get -y autoremove \
      && apt-get clean \
      && rm -rf /var/lib/apt/lists/*

RUN set -e \
      && curl -SL \
        http://sourceforge.net/projects/snpeff/files/snpEff_latest_core.zip \
        -o /tmp/snpeff.zip \
      && unzip -d /opt /tmp/snpeff.zip \
      && rm -f /tmp/snpeff.zip

RUN set -e \
      && mkdir /opt/snpEff/bin /opt/clinEff/bin \
      && echo '#!/usr/bin/env bash' > /opt/snpEff/bin/snpEff \
      && echo 'java -jar /opt/snpEff/snpEff.jar ${@}' \
        >> /opt/snpEff/bin/snpEff \
      && echo '#!/usr/bin/env bash' > /opt/snpEff/bin/SnpSift \
      && echo 'java -jar /opt/snpEff/SnpSift.jar ${@}' \
        >> /opt/snpEff/bin/SnpSift \
      && echo '#!/usr/bin/env bash' > /opt/clinEff/bin/ClinEff \
      && echo 'java -jar /opt/clinEff/ClinEff.jar ${@}' \
        >> /opt/clinEff/bin/ClinEff \
      && chmod +x /opt/snpEff/bin/* /opt/clinEff/bin/*

ENV PATH /opt/snpEff/bin:/opt/clinEff/bin:${PATH}

ENTRYPOINT ["/usr/bin/java", "-jar", "/opt/snpEff/snpEff.jar"]
