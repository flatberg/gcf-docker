FROM gcfntnu/bcl2fastq:latest

ENV CELLRANGER_ATAC_VER 2.0.0
ENV PATH /opt/cellranger-atac-$CELLRANGER_ATAC_VER:$PATH

COPY files/cellranger-atac-$CELLRANGER_ATAC_VER.tar.gz /opt/cellranger-atac-$CELLRANGER_ATAC_VER.tar.gz

RUN apt-get update --fix-missing &&  apt-get install -y ca-certificates && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

RUN \
  cd /opt && \
  tar -xzvf cellranger-atac-$CELLRANGER_ATAC_VER.tar.gz && \
  rm -rf /opt/cellranger-atac-$CELLRANGER_ATAC_VER.tar.gz


RUN \
  mkdir -p /opt/gffread && \
  cd /opt/gffread && \
  git clone https://github.com/gpertea/gclib && \
  git clone https://github.com/gpertea/gffread && \
  cd gffread && \
  make release

ENV PATH /opt/gffread/gffread:$PATH
