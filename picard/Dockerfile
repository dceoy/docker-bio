FROM java:jre

ADD https://github.com/broadinstitute/picard/archive/master.tar.gz /tmp/picard.tar.gz

RUN set -e \
      && tar xvf /tmp/picard.tar.gz -C /usr/local/src \
      && cd /usr/local/src/picard-master \
      && ./gradlew shadowJar

ENTRYPOINT ["java", "-jar", "/usr/local/src/picard-master/build/libs/picard.jar"]
