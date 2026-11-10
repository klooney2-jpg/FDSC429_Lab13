FROM mcr.microsoft.com/devcontainers/base:ubuntu

RUN apt-get update && apt-get install -y \
    wget \
    curl \
    git \
    unzip \
    pigz \
    parallel \
    openjdk-17-jre \
    python3 \
    python3-pip \
    ncbi-blast+ \
    fastqc \
    samtools \
    bcftools \
    minimap2 \
    && apt-get clean

# Install Miniforge
RUN wget -O Miniforge.sh \
    https://github.com/conda-forge/miniforge/releases/latest/download/Miniforge3-Linux-x86_64.sh && \
    bash Miniforge.sh -b -p /opt/conda && \
    rm Miniforge.sh

ENV PATH="/opt/conda/bin:${PATH}"

RUN conda install -y -n base -c conda-forge mamba

# Create bioinformatics environment
RUN mamba create -y -n bioinfo \
    -c conda-forge \
    -c bioconda \
    spades \
    quast \
    seqtk \
  #  trimmomatic \
  #  multiqc \
    seqsero2

RUN echo "source /opt/conda/etc/profile.d/conda.sh" >> /home/vscode/.bashrc && \
    echo "conda activate bioinfo" >> /home/vscode/.bashrc
