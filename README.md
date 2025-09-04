# aggregate-gene-expression-hshim1

Workflow created by: Ha-Na Shim
Date: 09/03/2025

## Tools/packages used

## Tools / Packages Used

<!-- Horizontal badges -->
[![R][R-badge]][R-url] 
[![RStudio][RStudio-badge]][RStudio-url] 
[![tidyverse][tidyverse-badge]][tidyverse-url] 
[![ggplot2][ggplot2-badge]][ggplot2-url] 
[![biomaRt][biomaRt-badge]][biomaRt-url] 
[![clusterProfiler][clusterProfiler-badge]][clusterProfiler-url] 
[![MSigDB][MSigDB-badge]][MSigDB-url] 
[![KEGG][KEGG-badge]][KEGG-url] 
[![Reactome][Reactome-badge]][Reactome-url] 

<p align="center">

<!-- R + RStudio -->
<a href="https://posit.co/products/open-source/rstudio/">
  <img src="https://raw.githubusercontent.com/rstudio/hex-stickers/main/PNG/RStudio.png" height="125" alt="RStudio hex">
</a>

<!-- tidyverse family -->
<a href="https://ggplot2.tidyverse.org/">
  <img src="https://raw.githubusercontent.com/rstudio/hex-stickers/main/SVG/ggplot2.svg" height="125" alt="ggplot2 hex">
</a>
<a href="https://www.tidyverse.org/">
  <img src="https://raw.githubusercontent.com/rstudio/hex-stickers/main/SVG/tidyverse.svg" height="125" alt="tidyverse hex">
</a>

<!-- Bioconductor packages -->
<a href="https://bioconductor.org/packages/biomaRt">
  <img src="https://raw.githubusercontent.com/Bioconductor/BiocStickers/master/biomaRt/biomaRt.png" height="125" alt="biomaRt hex">
</a>
<a href="https://bioconductor.org/packages/clusterProfiler">
  <img src="https://raw.githubusercontent.com/Bioconductor/BiocStickers/master/clusterProfiler/clusterProfiler.png" height="125" alt="clusterProfiler hex">
</a>

</p>

<!-- Badge image refs -->
[R-badge]: https://img.shields.io/badge/R-276DC3?style=for-the-badge&logo=r&logoColor=white
[RStudio-badge]: https://img.shields.io/badge/RStudio-75AADB?style=for-the-badge&logo=rstudio&logoColor=white
[tidyverse-badge]: https://img.shields.io/cran/v/tidyverse?style=for-the-badge&label=tidyverse
[ggplot2-badge]: https://img.shields.io/cran/v/ggplot2?style=for-the-badge&label=ggplot2
[biomaRt-badge]: https://img.shields.io/badge/biomaRt-Bioconductor-3C8DBC?style=for-the-badge
[clusterProfiler-badge]: https://img.shields.io/badge/clusterProfiler-Bioconductor-3C8DBC?style=for-the-badge
[MSigDB-badge]: https://img.shields.io/badge/MSigDB-Molecular%20Signatures%20Database-orange?style=for-the-badge
[KEGG-badge]: https://img.shields.io/badge/KEGG-Pathways-009688?style=for-the-badge
[Reactome-badge]: https://img.shields.io/badge/Reactome-Pathway%20Database-006699?style=for-the-badge

<!-- Link refs -->
[R-url]: https://www.r-project.org/
[RStudio-url]: https://posit.co/products/open-source/rstudio/
[tidyverse-url]: https://www.tidyverse.org/
[ggplot2-url]: https://ggplot2.tidyverse.org/
[biomaRt-url]: https://bioconductor.org/packages/biomaRt/
[clusterProfiler-url]: https://bioconductor.org/packages/clusterProfiler/
[MSigDB-url]: https://www.gsea-msigdb.org/gsea/msigdb
[KEGG-url]: https://www.genome.jp/kegg/
[Reactome-url]: https://reactome.org/



## About this repository
A lightweight and simple workflow/pipeline in R for extracting gene lists of interest from the gene ontology (GO) and MSigDB collections, as well as visualization of aggregate gene expression of a group of genes between conditions/treatments over time.

## Required packages and dependencies

## Functions in this repository

extract_GO_genes
extract_msigdb_genes
compile_gene_lists

<h2>Extracting GO Gene Sets with <code>extract_GO_genes</code></h2>

<p>
Use <code>extract_GO_genes()</code> to retrieve genes associated with one or more Gene Ontology (GO) terms from Ensembl BioMart.
It can optionally expand each term to include <strong>descendant terms</strong> in the GO hierarchy, supports <strong>BP / MF / CC</strong> ontologies,
and returns results as a <em>list</em>, <em>vector</em>, or <em>data.frame</em>.
</p>

<pre>
<code class="language-r">
# Example: Biological process "muscle structure development" (GO:0061061)
muscle_development <- extract_GO_genes(
  "GO:0061061",
  include_descendants = TRUE,
  organism = "human",
  ontology = "BP",
  output_format = "list",
  export_csv = FALSE,
  output_dir = "GO_gene_lists/"
)
</code>
</pre>

<details>
  <summary><strong>Function overview</strong></summary>
  <ul>
    <li><strong>What it does:</strong> Connects to Ensembl BioMart and fetches genes annotated to the specified GO term(s).
        If <code>include_descendants = TRUE</code>, it expands the query to all descendant terms using <code>GO.db</code> and deduplicates gene symbols.</li>
    <li><strong>Why it’s useful:</strong> Produces <em>comprehensive, up-to-date</em> gene sets for biological concepts (e.g., “cell cycle”, “muscle development”).</li>
    <li><strong>Performance note:</strong> Requires an internet connection. Large GO terms may take longer depending on Ensembl server availability.</li>
  </ul>
</details>

<h3>Parameters</h3>

<table>
  <thead>
    <tr>
      <th>Parameter</th>
      <th>Type</th>
      <th>Default</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr><td><code>go_terms</code></td><td>character</td><td>—</td><td>One or more GO IDs (e.g., "GO:0061061").</td></tr>
    <tr><td><code>organism</code></td><td>character</td><td>"human"</td><td>"human" or "mouse". Sets Ensembl dataset.</td></tr>
    <tr><td><code>include_descendants</code></td><td>logical</td><td>TRUE</td><td>If TRUE, expands to include all descendant terms.</td></tr>
    <tr><td><code>ontology</code></td><td>character</td><td>"BP"</td><td>GO domain: "BP" (Biological Process), "MF", or "CC".</td></tr>
    <tr><td><code>output_format</code></td><td>character</td><td>"list"</td><td>"list" (default), "vector" (single GO), or "data.frame".</td></tr>
    <tr><td><code>export_csv</code></td><td>logical</td><td>FALSE</td><td>If TRUE, exports results as CSVs in <code>output_dir</code>.</td></tr>
    <tr><td><code>output_dir</code></td><td>character</td><td>"GO_gene_lists/"</td><td>Directory for CSV exports (created if missing).</td></tr>
  </tbody>
</table>

<h3>Return Value</h3>
<ul>
  <li><strong>Single term + "vector"</strong> → character vector of gene symbols</li>
  <li><strong>Single/multiple + "list"</strong> → named list of gene vectors (with metadata in <code>attr(result, "metadata")</code>)</li>
  <li><strong>"data.frame"</strong> → table with columns: gene_symbol, go_label, go_id, go_name</li>
</ul>

<pre>
<code class="language-r">
# Example: Accessing metadata
md <- attr(muscle_development, "metadata")
str(md[1])
</code>
</pre>

<hr>

<p><strong>References:</strong><br>
Ashburner et al., <em>Nat Genet</em>, 2000. <br>
The Gene Ontology Consortium, <em>Nucleic Acids Res</em>, 2019.
</p>




