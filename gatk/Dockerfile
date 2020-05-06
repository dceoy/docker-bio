FROM ubuntu:latest

ENV DEBIAN_FRONTEND noninteractive

ADD https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh /tmp/miniconda.sh
ADD https://raw.githubusercontent.com/dceoy/print-github-tags/master/print-github-tags /usr/local/bin/print-github-tags

RUN set -e \
      && ln -sf bash /bin/sh

RUN set -e \
      && apt-get -y update \
      && apt-get -y dist-upgrade \
      && apt-get -y install --no-install-recommends --no-install-suggests \
        bzip2 ca-certificates curl g++ gcc git libc6-dev libfreetype-dev \
        libpng-dev make openjdk-8-jre pkg-config r-base unzip \
      && apt-get -y autoremove \
      && apt-get clean \
      && rm -rf /var/lib/apt/lists/*

RUN set -e \
      && /bin/bash /tmp/miniconda.sh -b -p /opt/conda \
      && /opt/conda/bin/conda update -n base -c defaults conda \
      && /opt/conda/bin/conda clean -ya \
      && ln -s /opt/conda/etc/profile.d/conda.sh /etc/profile.d/conda.sh \
      && echo '. /opt/conda/etc/profile.d/conda.sh' >> ~/.bashrc \
      && echo 'conda activate base' >> ~/.bashrc \
      && rm -f /tmp/miniconda.sh

RUN set -eo pipefail \
      && chmod +x /usr/local/bin/print-github-tags \
      && print-github-tags --release --latest broadinstitute/gatk \
        | xargs -i curl -SL \
          https://github.com/broadinstitute/gatk/releases/download/{}/gatk-{}.zip \
          -o /tmp/gatk.zip \
      && unzip -d /opt /tmp/gatk.zip \
      && mv /opt/gatk-* /opt/gatk \
      && cd /opt/gatk \
      && mkdir /opt/gatk/bin \
      && ln -s /opt/gatk/gatk /opt/gatk/bin/gatk \
      && rm -f /tmp/gatk.zip

RUN set -e \
      && sed \
        -e 's/\(openssl\|pip\|python\|setuptools\|certifi\|wheel\|tk\|xz\|readline\|zlib\|sqlite\)=.*/\1/' \
        -e 's/\(gatk.*.zip\)/\/opt\/gatk\/\1/' \
        /opt/gatk/gatkcondaenv.yml > /tmp/gatkcondaenv.yml \
      && /opt/conda/bin/conda env create -n gatk -f /tmp/gatkcondaenv.yml \
      && echo "source activate gatk" >> /opt/gatk/gatkenv.rc \
      && echo "source /opt/gatk/gatk-completion.sh" >> /opt/gatk/gatkenv.rc \
      && /opt/conda/bin/conda clean -yaf \
      && find /opt/conda -follow -type f -name '*.a' -delete \
      && find /opt/conda -follow -type f -name '*.pyc' -delete \
      && rm -rf /root/.cache/pip

RUN set -eo pipefail \
      && print-github-tags --release --latest broadinstitute/gatk \
        | xargs -i curl -SL \
          https://raw.githubusercontent.com/broadinstitute/gatk/{}/scripts/docker/gatkbase/install_R_packages.R \
          -o /opt/gatk/install_R_packages.R \
      && Rscript /opt/gatk/install_R_packages.R

ENV PATH /opt/gatk/bin:/opt/conda/envs/gatk/bin:/opt/conda/bin:${PATH}

ENTRYPOINT ["/opt/gatk/bin/gatk"]
