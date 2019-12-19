FROM ubuntu:latest

ENV DEBIAN_FRONTEND noninteractive

ADD https://raw.githubusercontent.com/dceoy/print-github-tags/master/print-github-tags /usr/local/bin/print-github-tags

RUN set -e \
      && ln -sf /bin/bash /bin/sh

RUN set -e \
      && apt-get -y update \
      && apt-get -y dist-upgrade \
      && apt-get -y install --no-install-recommends --no-install-suggests \
        ca-certificates curl build-essential libgd-dev libpng-dev nginx perl \
        unzip zlib1g-dev \
      && apt-get -y autoremove \
      && apt-get clean \
      && rm -rf /var/lib/apt/lists/*

RUN set -e \
      && ln -sf /dev/stdout /var/log/nginx/access.log \
      && ln -sf /dev/stderr /var/log/nginx/error.log

RUN set -eo pipefail \
      && chmod +x /usr/local/bin/print-github-tags \
      && print-github-tags --release --latest GMOD/jbrowse \
        | cut -f 1 -d '-' \
        | xargs -i curl -SL \
          https://github.com/GMOD/jbrowse/releases/download/{}-release/JBrowse-{}.zip \
          -o /tmp/jbrowse.zip \
      && unzip -d /tmp /tmp/jbrowse.zip \
      && rm -rf /var/www/html \
      && mv /tmp/JBrowse-* /var/www/html \
      && cd /var/www/html \
      && ./setup.sh \
      && rm -f /tmp/jbrowse.zip

EXPOSE 80

CMD ["/usr/sbin/nginx", "-g", "daemon off;"]
