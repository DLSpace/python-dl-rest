FROM ubuntu:latest

LABEL author="sreedhar potturi <sreedhar.potturi@gmail.com>" io.openshift.s2i.scripts-url="image:///s2i/bin"

RUN apt-get -q update
RUN apt-get -y install \
    bash \
    git \
    curl \
    ca-certificates \
    bzip2 \
    unzip \
    python-dev \ 
    g++

# Configure environment
ENV CONDA_DIR=/opt/conda CONDA_VER=4.3.14
ENV PATH=$CONDA_DIR/bin:$PATH SHELL=/bin/bash LANG=C.UTF-8
ENV KERAS_BACKEND=theano

# Install conda
RUN mkdir -p $CONDA_DIR && \
    echo export PATH=$CONDA_DIR/bin:'$PATH' > /etc/profile.d/conda.sh && \
    curl https://repo.continuum.io/miniconda/Miniconda3-${CONDA_VER}-Linux-x86_64.sh  -o mconda.sh && \
    /bin/bash mconda.sh -f -b -p $CONDA_DIR && \
    rm mconda.sh && \
    $CONDA_DIR/bin/conda install --yes conda==${CONDA_VER} && \
    $CONDA_DIR/bin/conda install --yes numpy scipy mkl nose sphinx && \
    $CONDA_DIR/bin/pip install parameterized && \
    $CONDA_DIR/bin/conda install --yes theano pygpu keras && \
    $CONDA_DIR/bin/pip install Flask

RUN mkdir /s2i
COPY  s2i /s2i
