FROM ubuntu

RUN set -e \
      && apt-get -y update \
      && apt-get -y upgrade \
      && apt-get -y install default-jre unzip wget \
      && apt-get -y autoremove \
      && apt-get clean

RUN set -e \
      && wget http://sourceforge.net/projects/snpeff/files/snpEff_latest_core.zip -O /tmp/snpeff.zip \
      && unzip /tmp/snpeff.zip -d /usr/local/src \
      && rm -rf /tmp/snpeff.zip

ENTRYPOINT ["java", "-jar", "/usr/local/src/snpEff/snpEff.jar"]
