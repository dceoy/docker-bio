FROM gcc

ADD https://github.com/BenLangmead/bowtie2/archive/master.tar.gz /tmp/bowtie2.tar.gz
ADD http://ccb.jhu.edu/software/tophat/downloads/tophat-2.1.1.Linux_x86_64.tar.gz /tmp/tophat.tar.gz

RUN set -e \
      && apt-get -y update \
      && apt-get -y install libtbb-dev libboost-thread-dev \
      && apt-get clean

RUN set -e \
      && tar xvf /tmp/bowtie2.tar.gz -C /usr/local/src \
      && cd /usr/local/src/bowtie2-master \
      && make \
      && make install

RUN set -e \
      && tar xvf /tmp/tophat.tar.gz -C /usr/local/src \
      && mv /usr/local/src/tophat-* /usr/local/src/tophat \
      && find /usr/local/src/tophat -type f -maxdepth 1 -executable | xargs -i ln -s {} /usr/local/bin

ENTRYPOINT ["tophat"]
