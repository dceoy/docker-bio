FROM ubuntu:latest

ENV DEBIAN_FRONTEND noninteractive

ADD https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh /tmp/miniconda.sh
ADD https://bitbucket.org/MDukhan/yeppp/downloads/yeppp-1.0.0.tar.bz2 /tmp/yeppp-1.0.0.tar.bz2
ADD https://raw.githubusercontent.com/dceoy/print-github-tags/master/print-github-tags /usr/local/bin/print-github-tags

RUN set -e \
      && ln -sf bash /bin/sh

RUN set -e \
      && apt-get -y update \
      && apt-get -y dist-upgrade \
      && apt-get -y install --no-install-recommends --no-install-suggests \
        autoconf automake ca-certificates cmake curl g++ gcc git libbz2-dev \
        libc6-dev libcurl4-gnutls-dev libfreetype6 libgsl-dev liblzma-dev \
        libncurses5-dev libperl-dev libreadline-dev libssl-dev libz-dev make \
        unzip \
      && apt-get -y autoremove \
      && apt-get clean \
      && rm -rf /var/lib/apt/lists/*

RUN set -e \
      && /bin/bash /tmp/miniconda.sh -b -p /opt/conda \
      && /opt/conda/bin/conda update -n base -c defaults conda \
      && /opt/conda/bin/conda clean -ya \
      && ln -s /opt/conda/etc/profile.d/conda.sh /etc/profile.d/conda.sh \
      && echo '. /opt/conda/etc/profile.d/conda.sh' >> /etc/profile \
      && rm -f /tmp/miniconda.sh

ENV PATH /opt/conda/envs/smoove-env/bin:/opt/conda/bin:${PATH}

RUN set -e \
      && conda config --add channels defaults \
      && conda config --add channels bioconda \
      && conda config --add channels conda-forge \
      && conda create -n smoove-env \
        python=2.7 awscli numpy scipy cython pysam toolshed pyvcf pyfaidx \
        cyvcf2 svtyper svtools \
      && echo 'source activate smoove-env' >> /etc/profile \
      && conda clean -ya \
      && rm -rf /root/.cache/pip

RUN set -eo pipefail \
      && chmod +x /usr/local/bin/print-github-tags \
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
      && print-github-tags --release --latest samtools/bcftools \
        | xargs -i curl -SL \
          https://github.com/samtools/bcftools/releases/download/{}/bcftools-{}.tar.bz2 \
          -o /tmp/bcftools.tar.bz2 \
      && tar xvf /tmp/bcftools.tar.bz2 -C /usr/local/src --remove-files \
      && mv /usr/local/src/bcftools-* /usr/local/src/bcftools \
      && cd /usr/local/src/bcftools \
      && autoheader \
      && autoconf \
      && ./configure --enable-libgsl --enable-perl-filters \
      && make \
      && make install

RUN set -eo pipefail \
      && print-github-tags --release --latest --tar ebiggers/libdeflate \
        | xargs -i curl -SL {} -o /tmp/libdeflate.tar.gz \
      && tar xvf /tmp/libdeflate.tar.gz -C /usr/local/src --remove-files \
      && mv /usr/local/src/libdeflate-* /usr/local/src/libdeflate \
      && cd /usr/local/src/libdeflate \
      && make CFLAGS='-fPIC -O3' libdeflate.a \
      && cp libdeflate.a /usr/local/lib \
      && cp libdeflate.h /usr/local/include

RUN set -eo pipefail \
      && print-github-tags --release --latest root-project/root \
        | sed -e 's/-/\./g' \
        | xargs -i curl -SL \
          https://root.cern/download/root_{}.Linux-ubuntu18-x86_64-gcc7.4.tar.gz \
          -o /tmp/root.tar.gz \
      && tar xvf /tmp/root.tar.gz -C /opt --remove-files

ENV BCFTOOLS_PLUGINS /usr/local/src/bcftools/plugins
ENV ROOTSYS /opt/root
ENV PYTHONPATH ${ROOTSYS}/lib:${PYTHONPATH}

RUN set -eo pipefail \
      && print-github-tags --release --latest abyzovlab/CNVnator \
        | xargs -i curl -SL \
          https://github.com/abyzovlab/CNVnator/releases/download/{}/CNVnator_{}.zip \
          -o /tmp/cnvnator.zip \
      && unzip -d /usr/local/src /tmp/cnvnator.zip \
      && mv /usr/local/src/CNVnator_* /usr/local/src/cnvnator \
      && tar xvf /tmp/yeppp-1.0.0.tar.bz2 -C /usr/local/src/cnvnator --remove-files \
      && cd /usr/local/src/cnvnator/src \
      && ln -s /usr/local/src/samtools . \
      && source /opt/root/bin/thisroot.sh \
      && make LIBS='-lcrypto' \
        YEPPPLIBDIR='/usr/local/src/cnvnator/yeppp-1.0.0/binaries/linux/x86_64' \
        YEPPPINCLUDEDIR='/usr/local/src/cnvnator/yeppp-1.0.0/library/headers' \
      && find /usr/local/src/cnvnator/src -maxdepth 1 -type f -executable \
        -exec ln -s {} /usr/local/bin \; \
      && rm -f /tmp/cnvnator.zip

ENV LD_LIBRARY_PATH ${ROOTSYS}/lib:/usr/local/src/cnvnator/yeppp-1.0.0/binaries/linux/x86_64:${LD_LIBRARY_PATH}

RUN set -eo pipefail \
      && print-github-tags --release --latest arq5x/lumpy-sv \
        | tr -d v \
        | xargs -i curl -SL \
          https://github.com/arq5x/lumpy-sv/releases/download/{}/lumpy-sv.tar.gz \
          -o /tmp/lumpy-sv.tar.gz \
      && tar xvf /tmp/lumpy-sv.tar.gz -C /usr/local/src --remove-files \
      && cd /usr/local/src/lumpy-sv/lib/htslib \
      && autoheader \
      && autoconf \
      && make \
      && make install \
      && cd /usr/local/src/lumpy-sv \
      && make \
      && find /usr/local/src/lumpy-sv/bin -maxdepth 1 -type f -executable \
        -exec ln -s {} /usr/local/bin \;

RUN set -eo pipefail \
      && print-github-tags --release --latest base2genomics/batchit \
        | xargs -i curl -SL \
          https://github.com/base2genomics/batchit/releases/download/{}/batchit \
          -o /usr/local/bin/batchit \
      && print-github-tags --release --latest brentp/mosdepth \
        | xargs -i curl -SL \
          https://github.com/brentp/mosdepth/releases/download/{}/mosdepth \
          -o /usr/local/bin/mosdepth \
      && print-github-tags --release --latest brentp/duphold \
        | xargs -i curl -SL \
          https://github.com/brentp/duphold/releases/download/{}/duphold \
          -o /usr/local/bin/duphold \
      && print-github-tags --release --latest brentp/gsort \
        | xargs -i curl -SL \
          https://github.com/brentp/gsort/releases/download/{}/gsort_linux_amd64 \
          -o /usr/local/bin/gsort \
      && print-github-tags --release --latest brentp/bpbio \
        | xargs -i curl -SL \
          https://github.com/brentp/bpbio/releases/download/{}/bpbio_static \
          -o /usr/local/bin/bpbio \
      && print-github-tags --release --latest brentp/gargs \
        | xargs -i curl -SL \
          https://github.com/brentp/gargs/releases/download/{}/gargs_linux \
          -o /usr/local/bin/gargs \
      && print-github-tags --release --latest brentp/goleft \
        | xargs -i curl -SL \
          https://github.com/brentp/goleft/releases/download/{}/goleft_linux64 \
          -o /usr/local/bin/goleft \
      && print-github-tags --release --latest brentp/smoove \
        | xargs -i curl -SL \
          https://github.com/brentp/smoove/releases/download/{}/smoove \
          -o /usr/local/bin/smoove \
      && chmod +x \
        /usr/local/bin/batchit /usr/local/bin/mosdepth /usr/local/bin/duphold \
        /usr/local/bin/gsort /usr/local/bin/bpbio /usr/local/bin/gargs \
        /usr/local/bin/goleft /usr/local/bin/smoove

ENTRYPOINT ["/usr/local/bin/smoove"]
