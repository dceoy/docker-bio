FROM ubuntu

ADD https://raw.githubusercontent.com/broadinstitute/gatk-protected/master/scripts/install_R_packages.R /tmp/install_R_packages.R

RUN set -e \
      && apt-get -y update \
      && apt-get -y install software-properties-common \
      && add-apt-repository ppa:webupd8team/java \
      && apt-get -y update \
      && apt-get -y upgrade \
      && yes yes | apt-get -y install oracle-java8-installer \
      && apt-get -y install git python r-base \
      && apt-get -y autoremove \
      && apt-get clean

RUN set -e \
      && git clone --depth 1 https://github.com/broadinstitute/gatk.git /usr/local/src/gatk \
      && cd /usr/local/src/gatk \
      && ./gradlew localJar \
      && Rscript /tmp/install_R_packages.R \
      && rm -rf /tmp/*

ENTRYPOINT ["java", "-jar", "/usr/local/src/gatk/build/libs/gatk.jar"]
