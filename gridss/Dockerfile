FROM ubuntu:20.04

ENV DEBIAN_FRONTEND noninteractive

ADD https://raw.githubusercontent.com/dceoy/clir/master/install_clir.sh /tmp/install_clir.sh
ADD https://raw.githubusercontent.com/dceoy/print-github-tags/master/print-github-tags /usr/local/bin/print-github-tags

RUN set -e \
      && ln -sf bash /bin/sh

RUN set -e \
      && apt-get -y update \
      && apt-get -y dist-upgrade \
      && apt-get -y install --no-install-recommends --no-install-suggests \
        apt-transport-https apt-utils autoconf ca-certificates curl g++ gcc \
        gfortran git libblas-dev libbz2-dev libcurl4-gnutls-dev \
        libfontconfig1-dev libfreetype6-dev libfribidi-dev libgit2-dev \
        libharfbuzz-dev libjpeg-dev liblapack-dev liblzma-dev libncurses5-dev \
        libpng-dev libssh-dev libssl-dev libtiff5-dev libxml2-dev libz-dev \
        make openjdk-8-jre r-base unzip util-linux \
      && apt-get -y autoremove \
      && apt-get clean \
      && rm -rf /var/lib/apt/lists/*

RUN set -e \
      && bash /tmp/install_clir.sh --root \
      && clir update \
      && clir install --devt=cran \
        argparser assertthat BiocManager blob R.cache randomForest Rcpp \
        RSQLite stringdist stringr testthat tidyverse \
      && clir install --bioc \
        copynumber biomaRt BSgenome org.Hs.eg.db Rsamtools rtracklayer \
        StructuralVariantAnnotation TxDb.Hsapiens.UCSC.hg19.knownGene \
        TxDb.Hsapiens.UCSC.hg38.knownGene VariantAnnotation \
      && clir validate \
        argparser BSgenome rtracklayer stringdist stringr \
        StructuralVariantAnnotation testthat tidyverse \
      && rm -f /tmp/install_clir.sh

RUN set -eo pipefail \
      && chmod +x /usr/local/bin/print-github-tags \
      && print-github-tags --release --latest lh3/bwa \
        | tr -d v \
        | xargs -i curl -SL \
          https://github.com/lh3/bwa/releases/download/v{}/bwa-{}.tar.bz2 \
          -o /tmp/bwa.tar.gz \
      && tar xvf /tmp/bwa.tar.gz -C /usr/local/src --remove-files \
      && mv /usr/local/src/bwa-* /usr/local/src/bwa \
      && cd /usr/local/src/bwa \
      && make \
      && find /usr/local/src/bwa -maxdepth 1 -type f -executable \
        -exec ln -s {} /usr/local/bin \;

RUN set -eo pipefail \
      && print-github-tags --release --latest samtools/samtools \
        | xargs -i curl -SL \
          https://github.com/samtools/samtools/releases/download/{}/samtools-{}.tar.bz2 \
          -o /tmp/samtools.tar.bz2 \
      && tar xvf /tmp/samtools.tar.bz2 -C /usr/local/src --remove-files \
      && mv /usr/local/src/samtools-* /usr/local/src/samtools \
      && cd /usr/local/src/samtools \
      && autoheader \
      && autoconf \
      && ./configure \
      && make \
      && make install

RUN set -eo pipefail \
      && mkdir /opt/gridss \
      && cd /opt/gridss \
      && print-github-tags --release --latest PapenfussLab/gridss \
        | tr -d v \
        | xargs -i curl -SL \
          -O https://github.com/PapenfussLab/gridss/releases/download/v{}/gridss-{}-gridss-jar-with-dependencies.jar \
          -O https://github.com/PapenfussLab/gridss/releases/download/v{}/gridss.config.R \
          -O https://github.com/PapenfussLab/gridss/releases/download/v{}/gridss.sh \
          -O https://github.com/PapenfussLab/gridss/releases/download/v{}/gridss_annotate_insertions_repeatmaster.R \
          -O https://github.com/PapenfussLab/gridss/releases/download/v{}/gridss_somatic_filter.R \
          -O https://github.com/PapenfussLab/gridss/releases/download/v{}/libgridss.R \
      && mv gridss-*.jar gridss.jar \
      && chmod +x /opt/gridss/gridss.sh

ENTRYPOINT ["/opt/gridss/gridss.sh"]
