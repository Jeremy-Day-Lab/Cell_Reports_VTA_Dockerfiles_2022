FROM bioconductor/bioconductor_docker:RELEASE_3_11

# LABEL adds metadata to an image:
LABEL maintainer="Lara Ianov <lianov@uab.edu>"
LABEL description="An environment to reproduce snRNA-seq analysis from the Day lab VTA dataset"

RUN apt-get update && apt-get install -y \
    libhdf5-dev \
    libcurl4-openssl-dev \
    libssl-dev \
    libpng-dev \
    libboost-all-dev \
    libxml2-dev \
    openjdk-8-jdk \
    python3-dev \
    python3-pip \
    wget \
    git \
    libfftw3-dev \
    libgsl-dev \
    llvm-10

RUN LLVM_CONFIG=/usr/lib/llvm-10/bin/llvm-config pip3 install llvmlite
RUN pip3 install numpy
RUN pip3 install umap-learn
RUN git clone --branch v1.2.1 https://github.com/KlugerLab/FIt-SNE.git

#below needed for FIt-SNE
RUN g++ -std=c++11 -O3 FIt-SNE/src/sptree.cpp FIt-SNE/src/tsne.cpp FIt-SNE/src/nbodyfft.cpp -o bin/fast_tsne -pthread -lfftw3 -lm

#NOTE:
# 1) spatstat error Error: object ‘markvario’ is not exported by 'namespace:spatstat',
# known issue - see https://github.com/satijalab/seurat/issues/4226 &&
# https://github.com/satijalab/seurat/issues/4222
# (new Seurat versions should run ok, but for older follow issue 4226) 
# with upgrade='never' in Seurat, to not re-install spatstat
# 2) Specifying Rcpp packages needed for uwot 0.1.8

RUN R --no-restore --no-save -e "install.packages('remotes'); \
remotes::install_version('Rcpp', version='1.0.5', repos='https://cloud.r-project.org', dependencies=c('Depends', 'Imports', 'LinkingTo'), upgrade='never'); \
remotes::install_version('RcppAnnoy', version='0.0.16', repos='https://cloud.r-project.org', dependencies=c('Depends', 'Imports', 'LinkingTo'), upgrade='never'); \
remotes::install_version('uwot', version='0.1.8', repos='https://cloud.r-project.org', dependencies=c('Depends', 'Imports', 'LinkingTo'), upgrade='never'); \
remotes::install_version('spatstat', version='1.64-1', repos='https://cloud.r-project.org', dependencies=c('Depends', 'Imports', 'LinkingTo'), upgrade='never')"


# limma (and other BioC packages) versions are linked to Bioconductor 3.11
RUN R --no-restore --no-save -e "BiocManager::install(c('multtest', 'S4Vectors', 'SummarizedExperiment', 'SingleCellExperiment', 'MAST', 'DESeq2', 'BiocGenerics', 'GenomicRanges', 'IRanges', 'rtracklayer', 'monocle', 'Biobase', 'limma'))"

# here we for non-bioconductor packs we add additional Seurat dependendies, without specifying a version as these were not used
# in VTA analysis (thus default is fine) but provides additional usability of the Seurat package from this Docker image
RUN R --no-restore --no-save -e "install.packages(c('VGAM', 'R.utils', 'metap', 'Rfast2', 'ape', 'hdf5r'), repos='https://cloud.r-project.org', dependencies=c('Depends', 'Imports', 'LinkingTo'))"



RUN R --no-restore --no-save -e "remotes::install_version('pheatmap', version='1.0.12', repos='https://cloud.r-project.org', dependencies=c('Depends', 'Imports', 'LinkingTo'), upgrade='never'); \
remotes::install_version('reldist', version='1.6-6', repos='https://cloud.r-project.org', dependencies=c('Depends', 'Imports', 'LinkingTo'), upgrade='never'); \
remotes::install_version('Seurat', version='3.2.2',repos='https://cloud.r-project.org', dependencies=c('Depends', 'Imports', 'LinkingTo'), upgrade='never')"

