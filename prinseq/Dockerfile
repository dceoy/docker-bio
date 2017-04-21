FROM perl

ADD https://sourceforge.net/projects/prinseq/files/latest/download?source=files /tmp/prinseq.tar.gz

RUN set -e \
      && tar xvf /tmp/prinseq.tar.gz -C /usr/local/src \
      && mv /usr/local/src/prinseq-* /usr/local/src/prinseq \
      && chmod +x /usr/local/src/prinseq/*.pl \
      && ls /usr/local/src/prinseq/*.pl | xargs -i ln -s {} /usr/local/bin

ENTRYPOINT ["/usr/local/bin/perl", "/usr/local/src/prinseq/prinseq-lite.pl"]
