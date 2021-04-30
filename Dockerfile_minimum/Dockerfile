FROM bioconductor/bioconductor_docker:RELEASE_3_11

# LABEL adds metadata to an image:
LABEL maintainer="Lara Ianov <lianov@uab.edu>"
LABEL description="An environment to reproduce snRNA-seq analysis from the Day lab VTA dataset"

#NOTE:
# 1) spatstat error Error: object ‘markvario’ is not exported by 'namespace:spatstat',
# known issue - see https://github.com/satijalab/seurat/issues/4226 &&
# https://github.com/satijalab/seurat/issues/4222
# (new Seurat versions should run ok, but for older follow issue 4226) 
# with upgrade='never' in Seurat, to not re-install spatstat
# 2) Specifying Rcpp packages needed for uwot 0.1.8

RUN R -e "install.packages('remotes'); \
remotes::install_version('Rcpp', version='1.0.5', repos='https://cloud.r-project.org', dependencies=c('Depends', 'Imports', 'LinkingTo'), upgrade='never'); \
remotes::install_version('RcppAnnoy', version='0.0.16', repos='https://cloud.r-project.org', dependencies=c('Depends', 'Imports', 'LinkingTo'), upgrade='never'); \
remotes::install_version('uwot', version='0.1.8', repos='https://cloud.r-project.org', dependencies=c('Depends', 'Imports', 'LinkingTo'), upgrade='never'); \
remotes::install_version('spatstat', version='1.64-1', repos='https://cloud.r-project.org', dependencies=c('Depends', 'Imports', 'LinkingTo'), upgrade='never'); \
remotes::install_version('pheatmap', version='1.0.12', repos='https://cloud.r-project.org', dependencies=c('Depends', 'Imports', 'LinkingTo'), upgrade='never'); \
remotes::install_version('reldist', version='1.6-6', repos='https://cloud.r-project.org', dependencies=c('Depends', 'Imports', 'LinkingTo'), upgrade='never'); \
remotes::install_version('Seurat', version='3.2.2',repos='https://cloud.r-project.org', dependencies=c('Depends', 'Imports', 'LinkingTo'), upgrade='never')"

# limma version is linked to Bioconductor 3.11
RUN R -e "BiocManager::install(c('limma'))"
