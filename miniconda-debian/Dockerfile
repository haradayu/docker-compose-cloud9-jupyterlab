FROM ubuntu:16.04

MAINTAINER Kamil Kwiek <kamil.kwiek@continuum.io>
ARG pass="password"
ENV LANG=C.UTF-8 LC_ALL=C.UTF-8

RUN apt-get update --fix-missing && apt-get install -y wget bzip2 ca-certificates \
    libglib2.0-0 libxext6 libsm6 libxrender1 \
    git mercurial subversion

RUN echo 'export PATH=/opt/conda/bin:$PATH' > /etc/profile.d/conda.sh && \
    wget --quiet https://repo.continuum.io/miniconda/Miniconda3-4.4.10-Linux-x86_64.sh -O ~/miniconda.sh && \
    /bin/bash ~/miniconda.sh -b -p /opt/conda && \
    rm ~/miniconda.sh

ENV PATH /opt/conda/bin:$PATH
RUN conda install -y jupyterlab && jupyter lab --generate-config &&echo "c.NotebookApp.token = '$pass'" > /root/.jupyter/jupyter_notebook_config.py 

EXPOSE 8888
ENTRYPOINT ["jupyter","lab","--allow-root","--ip=0.0.0.0","--notebook-dir=/workspace","--no-browser"]