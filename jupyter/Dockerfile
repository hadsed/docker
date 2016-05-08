FROM ubuntu

RUN apt-get update && apt-get install -y \
    gcc-4.9 \
    gfortran \
    python2.7-dev \
    git \
    python-pip \
    python-setuptools \
    pkg-config \
    libhdf5-dev \
    python-h5py \
    libblas-dev \
    liblapack-dev \
    libfreetype6-dev \
    emacs24 \
&& apt-get clean \
&& rm -rf /var/lib/apt/lists/*

RUN pip install -U pip==8.1.1

RUN pip install \
    cython==0.23.4 \
    h5py==2.6.0 \
    numpy==1.8.2 \
    scipy==0.16.1 \
    pandas==0.16.2 \
    matplotlib==1.5.0 \
    seaborn==0.6.0 \
    ipython==4.1 \
    scikit-learn==0.17.1 \
    jupyter==1.0.0
    
RUN pip install beautifulsoup4

RUN pip install -U numpy==1.11.0

WORKDIR /root

# hack to make sure kernel doesn't crash -- bug with ipynb and docker
# Add Tini. Tini operates as a process subreaper for jupyter. This prevents
# kernel crashes.
ENV TINI_VERSION v0.6.0
ADD https://github.com/krallin/tini/releases/download/${TINI_VERSION}/tini /usr/bin/tini
RUN chmod +x /usr/bin/tini
ENTRYPOINT ["/usr/bin/tini", "--"]

CMD ["jupyter", "notebook"]
