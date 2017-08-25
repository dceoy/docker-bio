FROM java

ADD https://github.com/timflutre/trimmomatic/archive/master.tar.gz /tmp/trimmomatic.tar.gz

RUN set -e \
      && apt-get -y update \
      && apt-get -y upgrade \
      && apt-get -y install make \
      && apt-get clean

RUN set -e \
      && tar xvf /tmp/trimmomatic.tar.gz -C /usr/local/src \
      && cd /usr/local/src/trimmomatic-master \
      && make \
      && rm -rf /tmp/*

ENTRYPOINT ["java", "-jar", "/usr/local/src/trimmomatic-master/classes/trimmomatic.jar"]
