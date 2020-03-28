FROM ubuntu:latest

ENV DEBIAN_FRONTEND noninteractive

ADD https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh /tmp/miniconda.sh
ADD https://raw.githubusercontent.com/dceoy/print-github-tags/master/print-github-tags /usr/local/bin/print-github-tags

RUN set -e \
      && ln -sf /bin/bash /bin/sh

RUN set -e \
      && apt-get -y update \
      && apt-get -y install --no-install-recommends --no-install-suggests \
        apt-transport-https apt-utils ca-certificates gnupg \
      && echo "deb https://cloud.r-project.org/bin/linux/ubuntu bionic-cran35/" \
        > /etc/apt/sources.list.d/r.list \
      && apt-key adv --keyserver keyserver.ubuntu.com \
        --recv-keys E298A3A825C0D65DFD57CBB651716619E084DAB9 \
      && apt-get -y update \
      && apt-get -y dist-upgrade \
      && apt-get -y install --no-install-recommends --no-install-suggests \
        bzip2 ca-certificates curl git openjdk-8-jre g++ gcc libc6-dev make \
        r-base unzip \
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
          https://raw.githubusercontent.com/broadinstitute/gatk/{}/scripts/docker/gatkbase/install_R_packages.R \
        | R --vanilla

RUN set -eo pipefail \
      && print-github-tags --release --latest broadinstitute/gatk \
        | xargs -i curl -SL \
          https://github.com/broadinstitute/gatk/releases/download/{}/gatk-{}.zip \
          -o /tmp/gatk.zip \
      && unzip -d /usr/local/src /tmp/gatk.zip \
      && mv /usr/local/src/gatk-* /usr/local/src/gatk \
      && cd /usr/local/src/gatk \
      && ln -s /usr/local/src/gatk/gatk /usr/local/bin \
      && rm -f /tmp/gatk.zip

ENV PATH /opt/conda/envs/gatk/bin:/opt/conda/bin:${PATH}

RUN set -e \
      && conda env create -n gatk -f /usr/local/src/gatk/gatkcondaenv.yml \
      && echo 'source activate gatk' >> /usr/local/src/gatk/gatkenv.rc \
      && echo 'source /usr/local/src/gatk/gatk-completion.sh' \
        >> /usr/local/src/gatk/gatkenv.rc \
      && conda clean -ya \
      && rm -rf /root/.cache/pip

ENTRYPOINT ["/usr/local/bin/gatk"]
