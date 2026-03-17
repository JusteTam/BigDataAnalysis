# ESCC RNA-seq Analysis

## Project Description
This project contains an RNA-seq analysis of esophageal squamous cell carcinoma (ESCC) tumour and matched normal tissue samples.
The goal of the analysis was to identify differentially expressed genes, investigate their biological functions, and explore enriched pathways related to tumour development.

The analysis includes:
- Raw data quality control
- Read trimming and mapping
- Mapping quality assessment
- Gene expression quantification
- Differential expression analysis
- Functional enrichment analysis (GO and GSEA)
- Pathway visualization

The RNA-seq dataset used in this project was originally published in:

**Cao, W., et al. (2020)**  
Multi-faceted epigenetic dysregulation of gene expression promotes esophageal squamous cell carcinoma.  
Nature Communications, 11, 3675.  
https://doi.org/10.1038/s41467-020-17227-z

## Data Description
The dataset contains **paired-end RNA-seq reads** from ESCC tumour and matched normal tissue samples.

Samples used in the analysis:

- SRR11647687  
- SRR11647690  
- SRR11647693  
- SRR11647697  
- SRR11647700  
- SRR11647703  

Reference genome:
- **GRCh38 human genome**

Gene annotation:
- **GENCODE v49**

## Repository Structure

```
feature_counts/
    Gene expression count tables generated with featureCounts

mapped_data_quality/
    Mapping QC results (coverage, correlation, PCA, clipping, junctions)

HW1 komandu sarasas.txt
    All terminal commands used for preprocessing, mapping and QC

Biological_data_analysis.html
    R analysis results including plots and downstream analysis

README.md
    Project description and instructions
```


## Software and Tools Used

### Command-line tools
- HISAT2
- SAMtools
- FastQC
- MultiQC
- Trim Galore
- Subread (featureCounts)
- RSeQC

### R packages
- DESeq2
- ggplot2
- pheatmap
- clusterProfiler
- enrichplot
- aPEAR
- dplyr
- tibble
- ggrepel
- tidyr
- stringr
- org.Hs.eg.db
- msigdbr
- BiocParallel


## How to Reproduce the Analysis

### 1. Quality Control
Run **FastQC** on raw FASTQ files and summarize results with **MultiQC**.

### 2. Read Trimming
Remove adapters and low-quality bases using **Trim Galore**.

### 3. Read Mapping
Align trimmed reads to the **GRCh38 reference genome** using **HISAT2**.

### 4. BAM Processing
Convert SAM → BAM, sort, index, and mark duplicates using **SAMtools**.

### 5. Mapping Quality Assessment
Evaluate mapping quality using **RSeQC** tools:
- gene body coverage
- correlation analysis
- PCA
- inner distance
- clipping profile
- splice junction annotation

### 6. Gene Quantification
Count reads overlapping genes using **featureCounts**.

### 7. Differential Expression Analysis
Perform normalization and differential expression analysis using **DESeq2 in R**.

### 8. Functional Analysis
Functional interpretation of genes was performed using:
- Gene Ontology (GO) over-representation analysis
- Gene Set Enrichment Analysis (GSEA)
- Pathway clustering and visualization using **aPEAR**

### Files in this repository

- **HW1 komandu sarasas.txt** – contains all terminal commands used in the preprocessing pipeline  
- **Biological_data_analysis.html** – contains the R analysis, plots, and downstream results  
- **feature_counts/** – read count tables  
- **mapped_data_quality/** – mapping quality results
