FROM java:jdk

RUN set -e \
      && apt-get -y update \
      && apt-get -y install git python r-base \
      && apt-get clean

RUN set -e \
      && git clone https://github.com/broadinstitute/gatk.git /usr/local/src/gatk \
      && cd /usr/local/src/gatk \
      && ./gradlew installAll

ENTRYPOINT ["java", "-jar", "/usr/local/src/picard-master/build/libs/picard.jar"]
