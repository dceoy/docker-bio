FROM java:jdk

ADD https://github.com/broadinstitute/gatk/archive/master.tar.gz /tmp/gatk.tar.gz

RUN set -e \
      && apt-get -y update \
      && apt-get -y install git python r-base \
      && apt-get clean

RUN set -e \
      && tar xvf /tmp/gatk.tar.gz -C /usr/local/src \
      && cd /usr/local/src/gatk-master \
      && ./gradlew installAll

ENTRYPOINT ["java", "-jar", "/usr/local/src/picard-master/build/libs/picard.jar"]
