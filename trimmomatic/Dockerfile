FROM java:jre

ADD https://github.com/timflutre/trimmomatic/archive/master.tar.gz /tmp/trimmomatic.tar.gz

RUN set -e \
      && tar xvf /tmp/trimmomatic.tar.gz -C /usr/local/src \
      && cd /usr/local/src/trimmomatic-master \
      && make
      && make check
      && make install

ENTRYPOINT ["trimmomatic"]
