FROM ubuntu

ADD http://cole-trapnell-lab.github.io/cufflinks/assets/downloads/cufflinks-2.2.1.Linux_x86_64.tar.gz /tmp/cufflinks.tar.gz

RUN set -e \
      && tar xvf /tmp/cufflinks.tar.gz -C /usr/local/src \
      && find /usr/local/src/cufflinks* -type f -executable | xargs -i ln -s {} /usr/local/bin/

ENTRYPOINT ["cufflinks"]