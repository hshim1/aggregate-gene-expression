# aggregate-gene-expression-hshim1

Workflow created by: Ha-Na Shim
Date: 09/03/2025


## Tools/packages used

<!-- Horizontal badges -->
[![R][R-badge]][R-url] [![RStudio][RStudio-badge]][RStudio-url] [![pheatmap][pheatmap-badge]][pheatmap-url] [![ggplot2][ggplot2-badge]][ggplot2-url] [![tidyverse][tidyverse-badge]][tidyverse-url] [![nf-core][nfcore-badge]][nfcore-url] [![Snakemake][Snakemake-badge]][Snakemake-url] [![Salmon][Salmon-badge]][Salmon-url] [![Kallisto][Kallisto-badge]][Kallisto-url] [![MultiQC][MultiQC-badge]][MultiQC-url]

<p align="center">

<a href="https://bioconductor.org/packages/DESeq2">
  <img src="https://raw.githubusercontent.com/Bioconductor/BiocStickers/master/DESeq2/DESeq2.png" height="125" alt="DESeq2 hex">
</a>
<a href="https://bioconductor.org/packages/clusterProfiler">
  <img src="https://raw.githubusercontent.com/Bioconductor/BiocStickers/master/clusterProfiler/clusterProfiler.png" height="125" alt="clusterProfiler hex">
</a>

<!-- Tidyverse family (official hex-stickers repo) -->
<a href="https://ggplot2.tidyverse.org/">
  <img src="https://raw.githubusercontent.com/rstudio/hex-stickers/main/SVG/ggplot2.svg" height="125" alt="ggplot2 hex">
</a>
<a href="https://www.tidyverse.org/">
  <img src="https://raw.githubusercontent.com/rstudio/hex-stickers/main/SVG/tidyverse.svg" height="125" alt="tidyverse hex">
</a>
<a href="https://dplyr.tidyverse.org/">
  <img src="https://raw.githubusercontent.com/rstudio/hex-stickers/main/SVG/dplyr.svg" height="125" alt="dplyr hex">
</a>

<!-- Bioconductor hexes -->
</a>
<a href="https://bioconductor.org/packages/edgeR">
  <img src="https://raw.githubusercontent.com/Bioconductor/BiocStickers/master/edgeR/edgeR.png" height="125" alt="edgeR hex">
</a>

</p>

<!-- Badge image refs -->
[R-badge]: https://img.shields.io/badge/R-276DC3?style=for-the-badge&logo=r&logoColor=white
[RStudio-badge]: https://img.shields.io/badge/RStudio-75AADB?style=for-the-badge&logo=rstudio&logoColor=white
[pheatmap-badge]: https://img.shields.io/cran/v/pheatmap?style=for-the-badge&label=pheatmap
[ggplot2-badge]: https://img.shields.io/cran/v/ggplot2?style=for-the-badge&label=ggplot2
[tidyverse-badge]: https://img.shields.io/cran/v/tidyverse?style=for-the-badge&label=tidyverse
[nfcore-badge]: https://img.shields.io/badge/nf--core-pipelines-00A98F?style=for-the-badge
[Snakemake-badge]: https://img.shields.io/badge/Snakemake-workflows-3277a8?style=for-the-badge
[Salmon-badge]: https://img.shields.io/badge/Salmon-quantification-ff8066?style=for-the-badge
[Kallisto-badge]: https://img.shields.io/badge/kallisto-quantification-555555?style=for-the-badge
[MultiQC-badge]: https://img.shields.io/pypi/v/multiqc?style=for-the-badge&label=MultiQC

<!-- Link refs -->
[R-url]: https://www.r-project.org/
[RStudio-url]: https://posit.co/products/open-source/rstudio/
[pheatmap-url]: https://cran.r-project.org/package=pheatmap
[ggplot2-url]: https://ggplot2.tidyverse.org/
[tidyverse-url]: https://www.tidyverse.org/
[nfcore-url]: https://nf-co.re/
[Snakemake-url]: https://snakemake.readthedocs.io/
[Salmon-url]: https://combine-lab.github.io/salmon/
[Kallisto-url]: https://pachterlab.github.io/kallisto/
[MultiQC-url]: https://multiqc.info/

## About this repository
A lightweight and simple workflow/pipeline in R for extracting gene lists of interest from the gene ontology (GO) and MSigDB collections, as well as visualization of aggregate gene expression of a group of genes between conditions/treatments over time.

## Required packages and dependencies

## function to extract gene ontology ids from GO database

extract_GO_genes

#' The function connects to Ensembl BioMart to retrieve current gene annotations.
#' When \code{include_descendants = TRUE}, the function performs hierarchical 
#' expansion using the GO.db package to capture genes from all descendant terms,
#' providing comprehensive coverage of biological concepts.
#' 
#' Gene symbols are deduplicated and filtered to remove empty entries. The function
#' generates standardized variable names from GO term descriptions for consistent
#' downstream use.

compile_gene_lists
extract_msigdb_genes

