FROM mcr.microsoft.com/devcontainers/base:ubuntu

RUN apt-get update && apt-get install -y \
    wget \
    curl \
    git \
    unzip \
    default-jre \
    python3 \
    python3-pip \
    ncbi-blast+ \
    fastqc \
    fasttree \
    && apt-get clean

# Install Miniconda
RUN wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh \
    -O /tmp/miniconda.sh && \
    bash /tmp/miniconda.sh -b -p /opt/conda && \
    rm /tmp/miniconda.sh

ENV PATH="/opt/conda/bin:${PATH}"

# Create bioinformatics environment
RUN conda create -y -n bioinfo \
    -c conda-forge \
    -c bioconda \
    spades \
    quast \
    seqtk \
    seqsero2

SHELL ["conda", "run", "-n", "bioinfo", "/bin/bash", "-c"]

RUN echo "Bioinformatics environment installed"
