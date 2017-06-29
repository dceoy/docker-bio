FROM perl

COPY annovar.latest.tar.gz /tmp/annovar.latest.tar.gz

RUN set -e \
      && tar xvf /tmp/annovar.latest.tar.gz -C /usr/local/src \
      && find /usr/local/src/annovar -type f -maxdepth 1 -executable | xargs -i ln -s {} /usr/local/bin

ENTRYPOINT ["/usr/local/bin/perl", "/usr/local/src/annovar/annotate_variation.pl"]