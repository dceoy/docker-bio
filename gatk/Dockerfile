FROM maven

ADD https://github.com/broadgsa/gatk-protected/archive/master.tar.gz /tmp/gatk.tar.gz

RUN set -e \
      && tar xvf /tmp/gatk.tar.gz -C /usr/local/src \
      && cd /usr/local/src/gatk-protected-master \
      && mvn package

ENTRYPOINT ["java", "-jar", "/usr/local/src/gatk-protected-master/target/GenomeAnalysisTK.jar"]
