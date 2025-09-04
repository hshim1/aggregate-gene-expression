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

<!-- ====================================================== -->
<!--        Required Packages / Dependencies (R)           -->
<!-- ====================================================== -->

<h2 id="dependencies">Required packages / dependencies</h2>

<p>
  This workflow uses a small set of CRAN and Bioconductor packages.
</p>

<!-- ------------------------------- -->
<!-- Compact summary (what & source) -->
<!-- ------------------------------- -->
<table style="width:100%; border-collapse:collapse;">
  <thead>
    <tr>
      <th style="text-align:left; border-bottom:1px solid #ddd;">Package</th>
      <th style="text-align:left; border-bottom:1px solid #ddd;">Source</th>
      <th style="text-align:left; border-bottom:1px solid #ddd;">Purpose</th>
    </tr>
  </thead>
  <tbody>
    <tr><td><code>pheatmap</code></td><td>CRAN</td><td>Publication-quality heatmaps</td></tr>
    <tr><td><code>RColorBrewer</code></td><td>CRAN</td><td>Color palettes for figures</td></tr>
    <tr><td><code>dplyr</code></td><td>CRAN</td><td>Data manipulation (part of tidyverse)</td></tr>
    <tr><td><code>ggplot2</code></td><td>CRAN</td><td>Grammar of graphics plotting</td></tr>
    <tr><td><code>tidyverse</code></td><td>CRAN</td><td>Data science toolkit (ggplot2, dplyr, readr, etc.)</td></tr>
    <tr><td><code>patchwork</code></td><td>CRAN</td><td>Compose multiple ggplots</td></tr>
    <tr><td><code>matrixStats</code></td><td>CRAN</td><td>Fast row/column summaries for matrices</td></tr>
    <tr><td><code>biomaRt</code></td><td>Bioconductor</td><td>Programmatic access to Ensembl</td></tr>
    <tr><td><code>clusterProfiler</code></td><td>Bioconductor</td><td>Enrichment analysis (GO/KEGG/Reactome/MSigDB)</td></tr>
    <tr><td><code>org.Hs.eg.db</code></td><td>Bioconductor</td><td>Human gene annotations</td></tr>
    <tr><td><code>org.Mm.eg.db</code></td><td>Bioconductor</td><td>Mouse gene annotations</td></tr>
    <tr><td><code>BiocManager</code></td><td>CRAN</td><td>Installer for Bioconductor packages</td></tr>
  </tbody>
</table>

## Repository structure

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

<!-- ======================================================= -->
<!--        MSigDB Gene Set Extraction: README Section       -->
<!-- ======================================================= -->

<h2 id="extract-msigdb-genes">Extracting Gene Sets with <code>extract_msigdb_genes</code></h2>

<p>
  <strong>Purpose.</strong> <code>extract_msigdb_genes()</code> pulls gene sets from the
  <a href="https://www.gsea-msigdb.org/gsea/msigdb/" target="_blank" rel="noopener">Molecular Signatures Database (MSigDB)</a>
  and returns clean vectors or named lists ready for enrichment analyses (GSEA/fgsea, clusterProfiler) and figure workflows.
  You can search by exact set names (e.g., <code>HALLMARK_APOPTOSIS</code>) or by a broad pattern (e.g., <code>"apoptosis"</code>),
  restrict to specific collections (Hallmark, KEGG, Reactome, GO), choose your preferred ID type (SYMBOL/ENTREZID/ENSEMBL),
  and optionally convert across organisms (human ↔ mouse).
</p>

<!-- ============== -->
<!-- Quick examples -->
<!-- ============== -->
<h3>Quick usage</h3>

<pre>
<code class="language-r">
# Hallmark (human, SYMBOLs)
apoptosis_genes &lt;- extract_msigdb_genes(
  gene_sets = "HALLMARK_APOPTOSIS",
  organism = "human",
  gene_id_type = "SYMBOL"
)

# KEGG glycolysis, restricting to canonical pathways (C2 &gt; CP:KEGG)
kegg_glycolysis &lt;- extract_msigdb_genes(
  gene_sets = "GLYCOLYSIS",
  search_all_collections = FALSE,
  collection = "C2",
  subcollection = "CP:KEGG"
)

# Reactome WNT, ENTREZ IDs
reactome_wnt &lt;- extract_msigdb_genes(
  gene_sets = "SIGNALING_BY_WNT",
  gene_id_type = "ENTREZID",
  search_all_collections = FALSE,
  collection = "C2",
  subcollection = "CP:REACTOME"
)

# Mouse Hallmark inflammatory response
mouse_inflammation &lt;- extract_msigdb_genes(
  gene_sets = "HALLMARK_INFLAMMATORY_RESPONSE",
  organism = "mouse"
)

# Cross-species conversion (human -&gt; mouse)
mouse_emt &lt;- extract_msigdb_genes(
  gene_sets = "HALLMARK_EPITHELIAL_MESENCHYMAL_TRANSITION",
  organism = "human",
  convert_organism = TRUE,
  target_organism = "mouse"
)

# Multiple sets + metadata inspection
sets    &lt;- c("HALLMARK_P53_PATHWAY", "HALLMARK_HYPOXIA", "KEGG_CELL_CYCLE")
results &lt;- extract_msigdb_genes(sets)
meta    &lt;- attr(results, "metadata")

# Summarize how many genes per set (requires dplyr installed)
dplyr::bind_rows(lapply(meta, as.data.frame), .id = "set_label")
</code>
</pre>

<!-- ================== -->
<!-- Parameter overview -->
<!-- ================== -->
<h3>Parameters</h3>

<table>
  <thead>
    <tr>
      <th style="min-width:160px;">Parameter</th>
      <th style="min-width:110px;">Type</th>
      <th style="min-width:110px;">Default</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><code>gene_sets</code></td>
      <td>character</td>
      <td>—</td>
      <td>Exact names (e.g., <code>"HALLMARK_APOPTOSIS"</code>) or case-insensitive patterns (e.g., <code>"APOPTOSIS"</code>). Single or vector.</td>
    </tr>
    <tr>
      <td><code>organism</code></td>
      <td>character</td>
      <td><code>"human"</code></td>
      <td><code>"human"</code> or <code>"mouse"</code> (maps to <em>Homo sapiens</em>/<em>Mus musculus</em> in <code>msigdbr</code>).</td>
    </tr>
    <tr>
      <td><code>gene_id_type</code></td>
      <td>character</td>
      <td><code>"SYMBOL"</code></td>
      <td>Output identifiers: <code>"SYMBOL"</code>, <code>"ENTREZID"</code>, or <code>"ENSEMBL"</code>.</td>
    </tr>
    <tr>
      <td><code>convert_organism</code></td>
      <td>logical</td>
      <td><code>FALSE</code></td>
      <td>If <code>TRUE</code>, converts the result to <code>target_organism</code> via BioMart homology.</td>
    </tr>
    <tr>
      <td><code>target_organism</code></td>
      <td>character</td>
      <td><em>NULL</em></td>
      <td>Required when <code>convert_organism = TRUE</code>; choose <code>"human"</code> or <code>"mouse"</code>.</td>
    </tr>
    <tr>
      <td><code>search_all_collections</code></td>
      <td>logical</td>
      <td><code>TRUE</code></td>
      <td>Search across all MSigDB collections. Set to <code>FALSE</code> to restrict using <code>collection</code>/<code>subcollection</code>.</td>
    </tr>
    <tr>
      <td><code>collection</code></td>
      <td>character</td>
      <td><em>NULL</em></td>
      <td>One of <code>H</code>, <code>C1</code>, <code>C2</code>, <code>C3</code>, <code>C4</code>, <code>C5</code>, <code>C6</code>, <code>C7</code>, <code>C8</code> (when restricting).</td>
    </tr>
    <tr>
      <td><code>subcollection</code></td>
      <td>character</td>
      <td><em>NULL</em></td>
      <td>Optional subcategory (e.g., <code>CP:KEGG</code>, <code>CP:REACTOME</code>, <code>GO:BP</code>).</td>
    </tr>
    <tr>
      <td><code>export_csv</code></td>
      <td>logical</td>
      <td><code>FALSE</code></td>
      <td>If <code>TRUE</code>, writes each set to CSV in <code>output_dir</code>.</td>
    </tr>
    <tr>
      <td><code>output_dir</code></td>
      <td>character</td>
      <td><code>"MSigDB_gene_lists/"</code></td>
      <td>Destination for CSV export (created if missing).</td>
    </tr>
  </tbody>
</table>

<!-- ============== -->
<!-- Return values  -->
<!-- ============== -->
<h3>Return value</h3>

<ul>
  <li><strong>Single match:</strong> a character vector of gene identifiers (format per <code>gene_id_type</code>).</li>
  <li><strong>Multiple matches:</strong> a named list of vectors. Rich metadata is attached at
    <code>attr(result, "metadata")</code>:
    <code>original_query</code>, <code>gene_set_name</code>, <code>collection</code>, <code>subcollection</code>,
    <code>n_genes</code>, <code>organism</code>, <code>gene_id_type</code>, <code>query_date</code>.
  </li>
</ul>

<pre>
<code class="language-r">
# Example: collect metadata into a data frame
res  &lt;- extract_msigdb_genes(c("HALLMARK_APOPTOSIS", "HALLMARK_HYPOXIA", "REACTOME_TCA_CYCLE"))
meta &lt;- attr(res, "metadata")
summary_df &lt;- dplyr::bind_rows(lapply(meta, as.data.frame), .id = "set_label")
summary_df
</code>
</pre>

<!-- ===== -->
<!-- Tips  -->
<!-- ===== -->
<h3>Practical notes</h3>

<ul>
  <li><strong>Pattern matching.</strong> If your query is a broad pattern (e.g., <code>"CELL_CYCLE"</code>), the function lists all matches and prefers exact set names when available. Otherwise, it selects the first match and reports alternatives.</li>
  <li><strong>ID formats.</strong> Choose the ID type that fits your downstream tools: SYMBOL for readability, ENTREZ for many enrichment functions, ENSEMBL for genomic work.</li>
  <li><strong>Cross-species.</strong> Homology mapping (human ↔ mouse) uses BioMart; not all genes map 1:1, so expect some dropouts or merges.</li>
  <li><strong>Exports.</strong> Set <code>export_csv = TRUE</code> to archive per-set CSVs alongside the analysis.</li>
  <li><strong>Versions &amp; licensing.</strong> Uses MSigDB via <code>msigdbr</code> (v2023.2+). Academic use is generally free; some curated sources (e.g., KEGG) may require a commercial license—check the
    <a href="https://www.gsea-msigdb.org/gsea/msigdb/" target="_blank" rel="noopener">MSigDB site</a>.
  </li>
</ul>

<!-- ========= -->
<!-- See also  -->
<!-- ========= -->
<h3>See also</h3>
<ul>
  <li><a href="https://cran.r-project.org/package=msigdbr" target="_blank" rel="noopener">msigdbr (CRAN)</a> — MSigDB access from R</li>
  <li><a href="https://www.gsea-msigdb.org/gsea/msigdb/human/genesets.jsp" target="_blank" rel="noopener">MSigDB Human Gene Sets</a> — browse collections</li>
  <li><a href="https://bioconductor.org/packages/biomaRt" target="_blank" rel="noopener">biomaRt</a> — organism conversion (homology)</li>
</ul>

<!-- =========== -->
<!-- References  -->
<!-- =========== -->
<h3>References</h3>
<ul>
  <li>Liberzon A. <em>et&nbsp;al.</em> The MSigDB hallmark gene set collection. <em>Cell Systems</em>. 2015;1(6):417–425.</li>
  <li>Subramanian A. <em>et&nbsp;al.</em> Gene set enrichment analysis. <em>PNAS</em>. 2005;102(43):15545–15550.</li>
</ul>

<!-- Small footnote for implementers -->
<p style="font-size:0.9em;color:#666;margin-top:0.75rem;">
  <em>Implementation note.</em> Cross-species conversion in examples assumes a helper like <code>convert_gene_list()</code> is available in your codebase (BioMart-backed). Adjust to your preferred orthology strategy as needed.
</p>


