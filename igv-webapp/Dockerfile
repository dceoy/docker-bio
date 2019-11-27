FROM ubuntu:latest

ENV DEBIAN_FRONTEND noninteractive

ADD https://raw.githubusercontent.com/dceoy/print-github-tags/master/print-github-tags /usr/local/bin/print-github-tags

RUN set -e \
      && apt-get -y update \
      && apt-get -y dist-upgrade \
      && apt-get -y install --no-install-recommends --no-install-suggests \
        ca-certificates curl git npm \
      && apt-get -y autoremove \
      && apt-get clean \
      && rm -rf /var/lib/apt/lists/*

RUN set -e \
      && npm install -g npm

RUN set -e \
      && chmod +x /usr/local/bin/print-github-tags \
      && print-github-tags --latest --tar igvteam/igv-webapp \
        | xargs -i curl -SL {} -o /tmp/igv-webapp.tar.gz \
      && tar xvf /tmp/igv-webapp.tar.gz -C /usr/local/src --remove-files \
      && mv /usr/local/src/igv-webapp-* /usr/local/src/igv-webapp \
      && cd /usr/local/src/igv-webapp \
      && sed -ie 's/http-server -a localhost dist/http-server -a 0.0.0.0 dist/' package.json \
      && rm package.jsone \
      && npm install \
      && npm run build

EXPOSE 8080

ENTRYPOINT ["npm", "start", "--prefix=/usr/local/src/igv-webapp"]
