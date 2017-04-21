FROM gcc

ADD https://github.com/infphilo/tophat/master.tar.gz /tmp/tophat.tar.gz

RUN set -e \
      && tar xvf /tmp/tophat.tar.gz -C /usr/local/src \
      && cd /usr/local/src/tophat-master \
      && ./configure \
      && make \
      && make check \
      && make install

ENTRYPOINT ["tophat"]
