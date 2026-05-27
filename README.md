# ESCC RNA-seq and DNA Methylation Analysis

## Project Description

This project contains an analysis of esophageal squamous cell carcinoma (ESCC) tumour and matched normal tissue samples.

The project includes two main parts:

1. **RNA-seq analysis**
   - Raw data quality control
   - Read trimming and mapping
   - Mapping quality assessment
   - Gene expression quantification
   - Differential expression analysis
   - Functional enrichment analysis
   - Pathway visualization

2. **Whole-genome bisulfite sequencing (WGBS) analysis**
   - Raw data quality control
   - Read trimming and mapping
   - M-bias assessment
   - DNA methylation calling
   - Methylation quality control
   - Differentially methylated cytosine analysis
   - Differentially methylated region analysis
   - Functional enrichment analysis

The aim of the project was to identify molecular differences between ESCC tumour and matched normal tissue samples, including changes in gene expression and DNA methylation patterns.

The dataset used in this project was originally published in:

**Cao, W., et al. (2020)**  
Multi-faceted epigenetic dysregulation of gene expression promotes esophageal squamous cell carcinoma.  
Nature Communications, 11, 3675.  
https://doi.org/10.1038/s41467-020-17227-z

---

## Data Description

### RNA-seq Data

The RNA-seq dataset contains paired-end RNA-seq reads from ESCC tumour and matched normal tissue samples.

Samples used in the RNA-seq analysis:

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

### WGBS Data

The WGBS dataset contains paired-end whole-genome bisulfite sequencing reads from ESCC tumour and matched normal esophageal tissue samples.

Samples used in the WGBS analysis:

- SRR11647652
- SRR11647653
- SRR11647662
- SRR11647663

Reference genome:

- **GRCh38 primary assembly**

The WGBS analysis was performed mainly on **chromosome 20**.

---

## Repository Structure

**feature_counts/**  
Gene expression count tables generated with featureCounts.

**mapped_data_quality/**  
Mapping QC results for the RNA-seq analysis, including gene body coverage, inner distance, clipping profile, annotated junctions, sample correlation and PCA.

**HW1 komandu sarasas.txt**  
Terminal commands used for RNA-seq preprocessing, mapping and QC.

**DE_analysis.html**  
R analysis results for RNA-seq differential expression and downstream analysis.

Inside **HW2_duomenys/**:

- **fastqc/**  
  FastQC quality-control reports for WGBS raw and/or trimmed sequencing reads.

- **mapped_data_quality/**  
  WGBS mapping and methylation quality-control results, including M-bias plots, coverage plots, correlation plots, PCA plots and other methylation QC outputs.

- **HW2_komandu_sarasas.txt**  
  Terminal commands used for WGBS data download, quality control, trimming, mapping, duplicate marking, M-bias analysis and methylation calling.

- **HW2_metilinimas.html**  
  HTML output containing the WGBS methylation analysis, including QC plots, DMC analysis, DMR analysis, annotation, visualization and enrichment results.


**README.md**  
Project description and instructions for reproducing the analysis.

---

## Software and Tools Used

### Command-line Tools

- HISAT2
- SAMtools
- FastQC
- MultiQC
- Trim Galore
- featureCounts
- RSeQC
- BSMAP
- Picard
- MethylDackel
- wget
- conda

### R Packages

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
- readr
- data.table
- bsseq
- DSS
- matrixTests
- ggvenn
- GenomicRanges
- annotatr
- TxDb.Hsapiens.UCSC.hg38.knownGene
- AnnotationDbi
- knitr
- scales

---

# RNA-seq Analysis Methods

## 1. Quality Control

Raw RNA-seq FASTQ files were checked using **FastQC**. The results were summarized using **MultiQC**.

## 2. Read Trimming

Adapters and low-quality bases were removed using **Trim Galore**.

## 3. Read Mapping

Trimmed reads were aligned to the **GRCh38 reference genome** using **HISAT2**.

## 4. BAM Processing

Mapped files were processed using **SAMtools**. SAM files were converted to BAM format, sorted and indexed.

## 5. Mapping Quality Assessment

Mapping quality was evaluated using **RSeQC** tools, including:

- gene body coverage
- inner distance
- clipping profile
- annotated junctions
- sample correlation
- PCA

## 6. Gene Quantification

Reads overlapping genes were counted using **featureCounts**.

## 7. Differential Expression Analysis

Differential expression analysis was performed in R using **DESeq2**. Count data were normalized and ESCC tumour samples were compared with matched normal tissue samples.

## 8. Functional Analysis

Functional interpretation of differentially expressed genes was performed using:

- Gene Ontology over-representation analysis
- Gene Set Enrichment Analysis
- pathway clustering and visualization using **aPEAR**

---

# WGBS DNA Methylation Analysis Methods

## 1. Data Download

Paired-end WGBS FASTQ files were downloaded from the European Nucleotide Archive using `wget`.

## 2. Quality Control

Raw WGBS reads were checked using **FastQC**.


## 3. Read Trimming

Adapters and low-quality bases were removed using **Trim Galore** in paired-end mode.
Trim Galore was run with quality filtering, gzip output and FastQC report generation.

## 4. Read Mapping

Trimmed WGBS reads were mapped to the **GRCh38 primary assembly** reference genome using **BSMAP**.


## 5. BAM Processing

Mapped BAM files were processed using **SAMtools** and **Picard**.

The main processing steps were:

- BAM files were sorted using SAMtools
- read groups were added using Picard AddOrReplaceReadGroups
- duplicate reads were marked using Picard MarkDuplicates

Duplicates were marked but not removed because preserving CpG coverage is important for methylation analysis.

## 6. M-bias Assessment

M-bias plots were generated using **MethylDackel**.


## 7. Methylation Calling

CpG methylation calls were extracted using **MethylDackel extract**.

Methylation extraction was performed on chromosome 20 using the GRCh38 reference genome. M-bias filtering parameters were applied during extraction to remove biased read positions.

## 8. Methylation Quality Control

Methylation calls were imported into R for quality control.

The following QC metrics were calculated:

- total number of reads per sample
- coverage distribution per CpG
- number of covered CpGs per sample
- Pearson correlation between samples
- PCA using methylation levels
- PCA using different coverage filters


## 9. Differentially Methylated Cytosine Analysis

Differentially methylated cytosines were identified using **DSS** in R.

Before testing, CpGs were filtered by coverage. Only CpGs where at least two samples had coverage of at least 10× were retained.


## 10. DMC Method Comparison

DMC calling using DSS was compared with a Wilcoxon test.


## 11. DMC Annotation and Visualization

DMCs were annotated using genomic features such as promoters, exons, introns, UTRs and intergenic regions.


## 12. Differentially Methylated Region Analysis

Differentially methylated regions were identified using **DSS callDMR**.

Several parameter sets were tested by changing:

- minimum number of CpGs per region
- minimum region length
- p-value threshold

The final parameter set was chosen to balance sensitivity and specificity.

## 13. Functional Enrichment Analysis

Genes associated with DMCs and DMRs were used for functional enrichment analysis.

Functional interpretation was performed using:

- Gene Ontology enrichment analysis
- KEGG pathway enrichment analysis
- clusterProfiler


