FROM gcfntnu/python-base-conda:3.7

ENV QUICKMIRSEQ_URL "https://downloads.sourceforge.net/project/quickmirseq/QuickMIRSeq.tgz"

RUN apt-get update --fix-missing && \
    apt-get install -y \
    sed \
    wget \
    unzip \
    bzip2

RUN conda install -y bowtie \
    cutadapt \
    mscorefonts \
    perl-compress-raw-zlib \
    perl-config-simple \
    perl-mime-base64 \
    perl-parallel-forkmanager \
    perl-xsloader \
    r-base==3.6.3 \
    r-reshape2 \
    r-ggplot2 \
    r-latticeExtra \
    r-scales

RUN wget --quiet $QUICKMIRSEQ_URL -O- | tar xzv -C /opt
WORKDIR /opt/QuickMIRSeq
RUN chmod +x -R .
RUN cp merge-tRNA.pl merge_tRNA.pl
RUN sed -e 's/ftp:/http:/' -e 's/release-83/release-100/' database/mouse/download.config > database/mouse/download.config
RUN sed -e 's/ftp:/http:/' -e 's/release-83/release-100/' database/human/download.config > database/human/download.config
RUN sed -e 's/ftp:/http:/' -e 's/release-83/release-100/' database/rat/download.config > database/rat/download.config

RUN grep -rl '^#!/usr/bin/perl' ./ | xargs sed -i '1s:#!/usr/bin/perl:#!/usr/bin/env perl:'

ENV QuickMIRSeq /opt/QuickMIRSeq
ENV PATH $QuickMIRSeq:$PATH