# aggregate-gene-expression-hshim1

Workflow created by: Ha-Na Shim
Date: 09/03/2025

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

# Part 1: Creating lists of genes of interest

<h2>Extracting GO Gene Sets with <code>extract_GO_genes</code></h2>

<p>
<code>extract_GO_genes()</code> provides functionality to retrieve gene lists associated with one or more Gene Ontology (GO) terms via Ensembl BioMart.
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

<p><strong>References:</strong><br>
Ashburner et al., <em>Nat Genet</em>, 2000. <br>
The Gene Ontology Consortium, <em>Nucleic Acids Res</em>, 2019.
</p>

<!-- ================================ -->
<!-- MSigDB (Molecular Signatures DB) -->
<!-- ================================ -->

<h2 id="msigdb-overview">MSigDB: Curated Gene Sets for Enrichment Analyses</h2>

<p>
  The <strong>Molecular Signatures Database (MSigDB)</strong> is a widely used collection of expert-curated and community-contributed gene sets designed for pathway and enrichment analyses (e.g., GSEA, fgsea, clusterProfiler). 
  It organizes thousands of gene sets into thematic collections—Hallmark biology, curated pathways (KEGG, Reactome, WikiPathways), regulatory targets, ontology terms, and more—so you can move from a list of differentially expressed genes to interpretable biology with confidence.
  Explore the human collections here: 
  <a href="https://www.gsea-msigdb.org/gsea/msigdb/human/genesets.jsp" target="_blank" rel="noopener noreferrer">
    gsea-msigdb.org › msigdb › human › genesets
  </a>.
</p>

<p>
  In practice, MSigDB shines when you need <em>clean, reproducible</em> definitions of pathways or biological programs—whether that’s a compact Hallmark signature for a figure, or a comprehensive GO category for a hypothesis test. The structure below shows how the database is organized; each collection groups gene sets with a shared purpose or source.
</p>

<hr>

<h3 id="msigdb-collections">MSigDB Collections (Human)</h3>

<!-- Tip: Use details/summary blocks for a tidy, scannable outline on GitHub -->
<details open>
  <summary><strong>H — Hallmark gene sets</strong> <em>(50 gene sets)</em></summary>
  <p style="margin: 0.5rem 0 0;">
    Compact, non-redundant “consensus” signatures that capture major biological states and processes.
  </p>
</details>

<details>
  <summary><strong>C1 — Positional gene sets</strong> <em>(302 gene sets)</em></summary>
  <p style="margin: 0.5rem 0 0;">
    Genes grouped by chromosomal location.
  </p>
  <p style="margin: 0.25rem 0 0;">
    <strong>Chromosomes:</strong> 1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18 19 20 21 22 X Y MT
  </p>
</details>

<details>
  <summary><strong>C2 — Curated gene sets</strong> <em>(7,561 gene sets)</em></summary>
  <ul>
    <li><strong>CGP</strong> — Chemical &amp; genetic perturbations <em>(3,538)</em></li>
    <li><strong>CP</strong> — Canonical pathways <em>(4,023)</em>, including:
      <ul>
        <li><strong>CP:BIOCARTA</strong> <em>(292)</em></li>
        <li><strong>CP:KEGG_MEDICUS</strong> <em>(658)</em></li>
        <li><strong>CP:PID</strong> <em>(196)</em></li>
        <li><strong>CP:REACTOME</strong> <em>(1,787)</em></li>
        <li><strong>CP:WIKIPATHWAYS</strong> <em>(885)</em></li>
        <li><strong>CP:KEGG_LEGACY</strong> <em>(186)</em></li>
      </ul>
    </li>
  </ul>
</details>

<details>
  <summary><strong>C3 — Regulatory gene sets</strong> <em>(3,713 gene sets)</em></summary>
  <ul>
    <li><strong>MIR</strong> — microRNA targets <em>(2,598)</em>
      <ul>
        <li><strong>MIR:MIRDB</strong> <em>(2,377)</em></li>
        <li><strong>MIR:MIR_LEGACY</strong> <em>(221)</em></li>
      </ul>
    </li>
    <li><strong>TFT</strong> — Transcription factor targets <em>(1,115)</em>
      <ul>
        <li><strong>TFT:GTRD</strong> <em>(505)</em></li>
        <li><strong>TFT:TFT_LEGACY</strong> <em>(610)</em></li>
      </ul>
    </li>
  </ul>
</details>

<details>
  <summary><strong>C4 — Computational gene sets</strong> <em>(1,006 gene sets)</em></summary>
  <ul>
    <li><strong>3CA</strong> — Curated Cancer Cell Atlas <em>(148)</em></li>
    <li><strong>CGN</strong> — Cancer gene neighborhoods <em>(427)</em></li>
    <li><strong>CM</strong> — Cancer modules <em>(431)</em></li>
  </ul>
</details>

<details>
  <summary><strong>C5 — Ontology gene sets</strong> <em>(16,228 gene sets)</em></summary>
  <ul>
    <li><strong>GO</strong> — Gene Ontology <em>(10,480)</em>
      <ul>
        <li><strong>GO:BP</strong> — Biological Process <em>(7,583)</em></li>
        <li><strong>GO:CC</strong> — Cellular Component <em>(1,042)</em></li>
        <li><strong>GO:MF</strong> — Molecular Function <em>(1,855)</em></li>
      </ul>
    </li>
    <li><strong>HPO</strong> — Human Phenotype Ontology <em>(5,748)</em></li>
  </ul>
</details>

<details>
  <summary><strong>C6 — Oncogenic signatures</strong> <em>(189 gene sets)</em></summary>
  <p style="margin: 0.5rem 0 0;">
    Gene sets capturing oncogene activation and cancer-relevant programs.
  </p>
</details>

<details>
  <summary><strong>C7 — Immunologic signatures</strong> <em>(5,219 gene sets)</em></summary>
  <ul>
    <li><strong>IMMUNESIGDB</strong> — ImmuneSigDB <em>(4,872)</em></li>
    <li><strong>VAX</strong> — Vaccine response signatures <em>(347)</em></li>
  </ul>
</details>

<details>
  <summary><strong>C8 — Cell type signatures</strong> <em>(866 gene sets)</em></summary>
  <p style="margin: 0.5rem 0 0;">
    Reference gene sets for cell identity and composition analyses.
  </p>
</details>

<p style="margin-top: 0.75rem; font-size: 0.9em; color: #666;">
  <em>Note.</em> Counts shown above reflect the breakdown provided for the human MSigDB collections. For the latest tallies and updates, see the official MSigDB site: 
  <a href="https://www.gsea-msigdb.org/gsea/msigdb/human/genesets.jsp" target="_blank" rel="noopener noreferrer">MSigDB Human Gene Sets</a>.
</p>



