# VTA Dockerfiles and image links

* “Minimum” version to reproduce VTA R code (tag 3.2.2): https://hub.docker.com/repository/docker/lianov/daylab_snrna

> An image made to reproduce the Day lab VTA analysis with minimum dependencies to re-run the code (e.g.: additional Seurat dependencies outside of the scope of the code shared is not present). 
> 
> Parent image from Bioconductor release 11.

Dockerfile in this repository at `./Dockerfile_minimum/Dockerfile`

* Minimum + additional Seurat dependencies not used in analysis but provides additional usage for exploratory purposes (tag 3.2.2): https://hub.docker.com/repository/docker/lianov/daylab_seurat_snrna

> An image made to reproduce the Day lab VTA analysis with minimum dependencies to re-run the code and a number of additional Seurat dependencies which were not used in the analysis (e.g.: DESeq2, multtest, metap which are needed for specific differential expression parameters or functions such as `FindConservedMarkers`) but can aid in the utilization of the container for exploratory purposes.
>
>Parent image from Bioconductor release 11.

Dockerfile in this repository at `./Dockerfile_additional_seurat_dependencies/Dockerfile`