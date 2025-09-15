
# Pipeline Results

## Overview

This directory contains all outputs from the microbiome probiotics RNA-Seq analysis pipeline, including both nf-core/rnaseq preprocessing results and downstream DESeq2 analysis outputs.

## nf-core/rnaseq Pipeline Outputs

The pipeline generates comprehensive quality control and quantification results:

## Directory Structure

### DESeq2 Analysis Outputs (`deseq2_R/`)

Results from R-based differential expression analysis:

```text
deseq2_R
├── dds_objects
│   ├── DESeq_data_C0.rds
│   ├── DESeq_data_CC_T0-1-2.rds
│   ├── DESeq_data_CCvCP_T0-1-2.rds
│   ├── DESeq_data_CCvCP-T0.rds
│   ├── DESeq_data_CCvCP-T1.rds
│   └── ...
├── GO_enrichment
│   ├── plot
│   │   ├── cnetplot
│   │   │   ├── GO_enrichment_cnetplot_C0.pdf
│   │   │   ├── GO_enrichment_cnetplot_CC_T0-1-2.pdf
│   │   │   ├── GO_enrichment_cnetplot_CCvCP_T0-1-2.pdf
│   │   │   └── ...
│   │   ├── dotplot
│   │   │   ├── GO_enrichment_dotplot_C0.pdf
│   │   │   ├── GO_enrichment_dotplot_CC_T0-1-2.pdf
│   │   │   ├── GO_enrichment_dotplot_CCvCP_T0-1-2.pdf
│   │   │   └── ...
│   │   └── GO_enrichment_comparisons.pdf
│   └── summary
│       ├── fisher
│       │   ├── fisher_results_C0.tsv
│       │   ├── fisher_results_CC_T0-1-2.tsv
│       │   ├── fisher_results_CCvCP_T0-1-2.tsv
│       │   └── ...
│       ├── GO_enrichment_C0.tsv
│       ├── GO_enrichment_CC_T0-1-2.tsv
│       ├── GO_enrichment_CCvCP_T0-1-2.tsv
│       └── ...
├── heatmap
│   ├── matrixes
│   │   ├── scaled_expression_matrix_T0.txt
│   │   ├── scaled_expression_matrix_T1.txt
│   │   ├── scaled_expression_matrix_T2.txt
│   │   └── scaled_expression_matrix.txt
│   └── plot
│       ├── heatmap_expressed_genes.png
│       ├── heatmap_expressed_genes_timepoint_T0.png
│       ├── heatmap_expressed_genes_timepoint_T1.png
│       └── heatmap_expressed_genes_timepoint_T2.png
├── Ordination_plot
│   └── plot
│       ├── ordination_plot.pdf
│       └── PCA_plot.pdf
├── permanova_results
│   ├── individual-matrix
│   │   ├── ALL_TIMEPOINTS_permanova_results.txt
│   │   ├── ALL_TREATMENTS_permanova_results.txt
│   │   ├── CCvCP_permanova_results.txt
│   │   └── ...
│   └── joined-matrix
│       ├── pairwise_permanova_results.txt
│       └── permanova_results.txt
└── summary
    ├── DEcounts
    │   ├── DESeq_summary_timepoint.tsv
    │   ├── DESeq_summary_Time.tsv
    │   ├── DESeq_summary_treatm_combination_times.tsv
    │   └── DESeq_summary_Treatment.tsv
    ├── DEgenes
    │   ├── DESeq_Comparison-ALL.tsv
    │   ├── DESeq_Comparison-CC_T0-1-2.tsv
    │   ├── DESeq_Comparison-CCvCP_T0-1-2.tsv
    │   ├── ...
    │   └── DESeq_counts_annotated.tsv
    ├── DESeq_individual_comp_summary_info.txt
    ├── DESeq_summary_info.txt
    └── DESeq_timepoints_summary_info.txt
```

### nf-core/rnaseq Main Outputs

Primary preprocessing and quantification results:

```text
├── fastp
│   ├── 2024_Pver_CC_T0_01_01.fastp.html
│   ├── 2024_Pver_CC_T0_01_01.fastp.json
│   ├── 2024_Pver_CC_T0_02_04.fastp.json
│   ├── ...
│   └── log
├── fastqc
│   ├── raw
│   └── trim
├── fq_lint
│   ├── raw
│   └── trimmed
├── multiqc
│   └── star_salmon
├── pipeline_info
│   ├── 'multiple logs'
├── salmon
│   ├── 2024_Pver_CC_T0_01_01
│   ├── 2024_Pver_CC_T0_02_04
│   ├── ...
│   ├── deseq2_qc
│   ├── salmon.merged.gene_counts_length_scaled.SummarizedExperiment.rds
│   ├── salmon.merged.gene_counts_length_scaled.tsv
│   ├── salmon.merged.gene_counts_scaled.SummarizedExperiment.rds
│   ├── salmon.merged.gene_counts_scaled.tsv
│   ├── salmon.merged.gene_counts.SummarizedExperiment.rds
│   ├── salmon.merged.gene_counts.tsv
│   ├── salmon.merged.gene_lengths.tsv
│   ├── salmon.merged.gene_tpm.tsv
│   ├── salmon.merged.transcript_counts.SummarizedExperiment.rds
│   ├── salmon.merged.transcript_counts.tsv
│   ├── salmon.merged.transcript_lengths.tsv
│   ├── salmon.merged.transcript_tpm.tsv
│   └── tx2gene.tsv
└── star_salmon
    ├── 2024_Pver_CC_T0_01_01
    ├── 2024_Pver_CC_T0_01_01.markdup.sorted.bam
    ├── 2024_Pver_CC_T0_01_01.markdup.sorted.bam.bai
    ├── ...
    ├── bigwig
    ├── deseq2_qc
    ├── dupradar
    ├── log
    ├── picard_metrics
    ├── qualimap
    ├── rseqc
    ├── salmon.merged.gene_counts_length_scaled.SummarizedExperiment.rds
    ├── salmon.merged.gene_counts_length_scaled.tsv
    ├── salmon.merged.gene_counts_scaled.SummarizedExperiment.rds
    ├── salmon.merged.gene_counts_scaled.tsv
    ├── salmon.merged.gene_counts.SummarizedExperiment.rds
    ├── salmon.merged.gene_counts.tsv
    ├── salmon.merged.gene_lengths.tsv
    ├── salmon.merged.gene_tpm.tsv
    ├── salmon.merged.transcript_counts.SummarizedExperiment.rds
    ├── salmon.merged.transcript_counts.tsv
    ├── salmon.merged.transcript_lengths.tsv
    ├── salmon.merged.transcript_tpm.tsv
    ├── samtools_stats
    ├── stringtie
    └── tx2gene.tsv
```

## Key Result Files

### For Downstream Analysis

- **Gene Counts:** `salmon/salmon.merged.gene_counts.tsv` - Raw gene count matrix
- **Gene TPM:** `salmon/salmon.merged.gene_tpm.tsv` - Normalized expression values  
- **Sample QC:** `multiqc/multiqc_report.html` - Comprehensive quality report

### DESeq2 Outputs

- **DEG Lists:** `deseq2_R/summary/DEgenes/` - Differentially expressed genes per comparison
- **Statistics:** `deseq2_R/summary/DEcounts/` - Summary statistics for each comparison
- **Visualizations:** `deseq2_R/*/plot/` - PCA plots, heatmaps, and other figures
- **GO Enrichment:** `deseq2_R/GO_enrichment/` - Functional enrichment results

## Analysis Workflow

1. **Quality Control:** Review `multiqc_report.html` for sample quality assessment
2. **Expression Data:** Use gene counts from `salmon/` directory for DESeq2 analysis  
3. **Differential Expression:** Run R scripts in `../Rscripts/` directory
4. **Results:** Examine outputs in `deseq2_R/` subdirectories

## References

- [nf-core/rnaseq documentation](https://nf-co.re/rnaseq)
- [DESeq2 Analysis Guide](../Rscripts/README.md)
