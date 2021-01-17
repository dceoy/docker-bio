FROM ubuntu:latest

ENV DEBIAN_FRONTEND noninteractive

ADD https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh /tmp/miniconda.sh

RUN set -e \
      && ln -sf bash /bin/sh

RUN set -e \
      && apt-get -y update \
      && apt-get -y dist-upgrade \
      && apt-get -y install --no-install-recommends --no-install-suggests \
        ca-certificates curl \
      && apt-get -y autoremove \
      && apt-get clean \
      && rm -rf /var/lib/apt/lists/*

RUN set -e \
      && /bin/bash /tmp/miniconda.sh -b -p /opt/conda \
      && /opt/conda/bin/conda update -n base -c defaults conda \
      && /opt/conda/bin/conda clean -ya \
      && ln -s /opt/conda/etc/profile.d/conda.sh /etc/profile.d/conda.sh \
      && echo '. /opt/conda/etc/profile.d/conda.sh' >> /etc/profile \
      && echo 'conda activate base' >> /etc/profile \
      && rm -f /tmp/miniconda.sh

ENV PATH /opt/conda/bin:${PATH}

RUN set -e \
      && conda config --add channels defaults \
      && conda config --add channels bioconda \
      && conda config --add channels conda-forge \
      && conda install gencore \
      && conda clean -ya \
      && rm -rf /root/.cache/pip

ENTRYPOINT ["/opt/conda/bin/gencore"]
