# Coral-priming RNA-Seq Analysis Pipeline

## Overview

This repository contains the host RNA-Seq analysis pipeline for the study *Pathogen priming reveals host immune training and microbiome conditioning in corals* (Monti et al., 2026, *ISME Host Microbe*; [doi:10.1093/ismehm/aazag001](https://doi.org/10.1093/ismehm/aazag001)). The RNA-Seq analysis here addresses the host gene expression modulation, including the immune and cellular responses, linked to priming.

The pipeline uses nf-core/rnaseq for preprocessing, quantification with Salmon, and DESeq2 for differential expression analysis.

## Citation

If you use this code or data, please cite:

> Monti M, Garcias-Bonet N, García FC, Santoro EP, Aljuaid G, Schuster K, Antony CP, Casartelli M, Beenham L, Giorgi A, Colin L, Voolstra CR, Peixoto RS (2026). Pathogen priming reveals host immune training and microbiome conditioning in corals. *ISME Host Microbe* 1(1): aazag001. https://doi.org/10.1093/ismehm/aazag001

**Experimental Design:**

- **Species:** *Pocillopora verrucosa* coral
- **Treatments:** Untouched control (CC), non-primed corals (CP), corals primed with inactivated *V. coralliilyticus* (VD) and corals primed with live *V. coralliilyticus* (VL)  
- **Timepoints:** T0 (baseline), T1, T2
- **Replicates:** 4 biological replicates per condition
- **Sequencing:** Paired-end RNA-Seq

**Folder structure:**

```text
.
├── README.md                 <- This file
├── input_fq/                 <- Raw paired-end FASTQ files
├── samplesheet.csv           <- Sample metadata for nf-core/rnaseq
├── nf-params.json            <- nf-core/rnaseq parameters 
├── nextflow.config           <- Nextflow configuration for local execution
├── Pver_ref/                 <- P. verrucosa reference genome and annotations
│   ├── GCF_036669915.1_ASM3666991v2_genomic.fna.gz  <- Reference genome
│   ├── genomic.simple.gtf.gz <- Simplified GTF annotation
│   └── README.md             <- Reference genome documentation
├── Rscripts/                 <- R scripts for downstream analysis
│   ├── DESeq2.r              <- Differential expression analysis
│   ├── GO_enrichment.r       <- Gene ontology enrichment
│   ├── Heatmap.r             <- Expression heatmaps
│   ├── Ordination_plot.r     <- PCA and ordination plots
│   ├── Permanova.r           <- PERMANOVA statistical analysis
│   └── README.md             <- R scripts documentation
├── results/                  <- Pipeline outputs (auto-generated)
│   ├── fastp/                <- Quality trimming results
│   ├── fastqc/               <- Quality control reports
│   ├── salmon/               <- Salmon quantification results
│   ├── star_salmon/          <- STAR alignment + Salmon quantification
│   ├── multiqc/              <- Aggregated QC report
│   ├── deseq2_R/             <- DESeq2 analysis outputs
│   └── README.md             <- Results documentation
└── work/                     <- Nextflow work directory (auto-generated)
```

## Pipeline Workflow

### 1. Setup and Installation

Install required tools:

```bash
# Install nf-core and Nextflow
pip install nf-core
curl -s https://get.nextflow.io | bash

# Or via conda/mamba
mamba install -c bioconda nextflow nf-core
```

### 2. Reference Genome Preparation

The pipeline uses *Pocillopora verrucosa* reference genome (GCF_036669915.1):

- **Genome:** `Pver_ref/GCF_036669915.1_ASM3666991v2_genomic.fna.gz`
- **Annotation:** `Pver_ref/genomic.simple.gtf.gz` (simplified for compatibility)

See [`Pver_ref/README.md`](Pver_ref/README.md) for detailed genome preparation steps.

### 3. Sample Preparation

Organize FASTQ files and create samplesheet:

```bash
# Generate samplesheet from FASTQ files
echo "sample,fastq_1,fastq_2,strandedness" > samplesheet.csv
for i in input_fq/*_1.fq.gz; do 
  sample=$(basename $i | sed 's/KAUST_//g' | sed 's/_1.fq.gz//g')
  fq1=$(readlink -f $i)
  fq2=$(readlink -f $i | sed 's/_1./_2./g')
  echo "${sample},${fq1},${fq2},auto" >> samplesheet.csv
done
```

### 4. Run nf-core/rnaseq Pipeline

Execute the main RNA-seq processing pipeline:

```bash
nextflow run nf-core/rnaseq \
  -r 3.18.0 \
  -name microbiome_probiotics_RNASeq \
  -profile singularity \
  -params-file nf-params.json
```

**Key Parameters:**

- **Trimmer:** fastp
- **Quantification:** Salmon (pseudo-alignment)
- **Reference:** P. verrucosa genome
- **Output:** Comprehensive QC and quantification results

### 5. Quality Control Review

Review generated reports:

- **MultiQC:** `results/multiqc/multiqc_report.html`
- **FastQC:** Individual sample QC in `results/fastqc/`
- **fastp:** Trimming reports in `results/fastp/`

### 6. Differential Expression Analysis

Run R-based downstream analysis:

```bash
# Setup R environment (optional)
mamba create -n r_env_DESeq2 -c conda-forge -c bioconda \
  r-base bioconductor-deseq2 r-ggplot2 r-dplyr \
  bioconductor-tximport r-patchwork

# Activate environment and run analysis
mamba activate r_env_DESeq2
Rscript Rscripts/DESeq2.r
```

**Analysis Components:**

- **DESeq2:** Differential expression between treatments/timepoints
- **GO Enrichment:** Functional enrichment analysis
- **Visualization:** PCA, heatmaps, volcano plots
- **Statistics:** PERMANOVA for treatment effects

### 7. Results and Interpretation

Key outputs in `results/deseq2_R/`:

- **DEG Lists:** Differentially expressed genes per comparison
- **GO Enrichment:** Functional categories affected
- **Visualizations:** PCA plots, heatmaps, network plots
- **Statistics:** PERMANOVA results for treatment significance

## Key Files and Documentation

- **Main Documentation:** [`README.md`](README.md) (this file)
- **Reference Genome Info:** [`Pver_ref/README.md`](Pver_ref/README.md)
- **R Scripts Documentation:** [`Rscripts/README.md`](Rscripts/README.md)  
- **Results Documentation:** [`results/README.md`](results/README.md)
- **Sample Metadata:** [`samplesheet.csv`](samplesheet.csv)
- **Pipeline Parameters:** [`nf-params.json`](nf-params.json)

## References

- [Monti et al. 2026, *ISME Host Microbe* (doi:10.1093/ismehm/aazag001)](https://doi.org/10.1093/ismehm/aazag001)
- [nf-core/rnaseq pipeline](https://nf-co.re/rnaseq/3.18.0)
- [DESeq2 Bioconductor package](https://bioconductor.org/packages/release/bioc/html/DESeq2.html)
- [Pocillopora verrucosa reference genome (GCF_036669915.1)](https://www.ncbi.nlm.nih.gov/datasets/genome/GCF_036669915.1/)
- [Salmon quantification tool](https://salmon.readthedocs.io/)
- [MultiQC aggregation tool](https://multiqc.info/)
