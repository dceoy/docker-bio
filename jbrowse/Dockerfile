FROM ubuntu:latest

ENV DEBIAN_FRONTEND noninteractive

RUN set -e \
      && apt-get -y update \
      && apt-get -y dist-upgrade \
      && apt-get -y install --no-install-recommends --no-install-suggests \
        ca-certificates curl build-essential libgd-dev libpng-dev nginx perl unzip zlib1g-dev \
      && apt-get -y autoremove \
      && apt-get clean \
      && rm -rf /var/lib/apt/lists/*

RUN set -e \
      && ln -sf /dev/stdout /var/log/nginx/access.log \
      && ln -sf /dev/stderr /var/log/nginx/error.log

RUN set -e \
      && curl -sS https://github.com/GMOD/jbrowse/releases/latest \
        | sed -e 's/^.*"\(https:\/\/github.com\/[^\/]\+\/[^\/]\+\/releases\/\)tag\/\([^"]\+\)-release".*$/\1download\/\2-release\/JBrowse-\2\.zip/' \
        | xargs -i curl -SL {} -o /tmp/jbrowse.zip \
      && unzip -d /tmp /tmp/jbrowse.zip \
      && rm -rf /var/www/html \
      && mv /tmp/JBrowse-* /var/www/html \
      && cd /var/www/html \
      && ./setup.sh \
      && rm -f /tmp/jbrowse.zip

EXPOSE 80

CMD ["/usr/sbin/nginx", "-g", "daemon off;"]
