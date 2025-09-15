# R Scripts for Differential Expression Analysis

## Overview

This directory contains R scripts for downstream analysis of the RNA-Seq data processed by the nf-core/rnaseq pipeline. The analysis focuses on differential expression between coral treatments (Control vs Coral Probiotics vs VD) across multiple timepoints (T0, T1, T2).

## Environment Setup

Create a conda environment with required R packages:

```bash
mamba create -n r_env_DESeq2 -c conda-forge -c bioconda \
  r-base bioconductor-deseq2 r-ellipse r-ggplot2 r-dplyr r-tidyr \
  r-data.table bioconductor-phyloseq r-patchwork r-ggrepel r-pacman \
  bioconductor-summarizedexperiment bioconductor-tximport \
  bioconductor-apeglm bioconductor-GenomicFeatures r-httpgd radian
```

- Import the count data into R.
- Perform differential expression analysis using DESeq2.
- Example R script:

  ```R
  library(DESeq2)
  countData <- read.csv("results/counts.csv", row.names = 1)
  colData <- read.csv("samplesheet.csv", row.names = 1)
  dds <- DESeqDataSetFromMatrix(countData = countData, colData = colData, design = ~ condition)
  dds <- DESeq(dds)
  results <- results(dds)
  ```

## Interpretation and Visualization

- Interpret the results and visualize them using tools like ggplot2 or pheatmap.

## Script Descriptions

- **DESeq2.r:** Main differential expression analysis comparing treatments and timepoints. Requires nf-core/rnaseq output. Results saved to `../results/deseq2_R/`
- **Ordination_plot.r:** Creates PCA and ordination visualizations. Depends on DESeq2.r output. Plots saved to `../results/deseq2_R/Ordination_plot/`
- **Heatmap.r:** Generates expression heatmaps for significant genes. Uses nf-core/rnaseq counts. Output in `../results/deseq2_R/heatmap/`
- **GO_enrichment.r:** Performs Gene Ontology enrichment analysis on DEGs. Depends on DESeq2.r results. Output in `../results/deseq2_R/GO_enrichment/`
- **Permanova.r:** Statistical analysis using PERMANOVA to test treatment effects. Uses DESeq2.r output. Results in `../results/deseq2_R/permanova_results/`

## References

- [DESeq2 documentation](https://bioconductor.org/packages/release/bioc/html/DESeq2.html)
