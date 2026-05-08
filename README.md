# mithunmicrobiomediet

# **README**

## **Overview**

This repository contains the code and data used to process and analyze the rumen microbiome and diet metabarcoding datasets for the mithun (*Bos frontalis*) seasonal variation study.

The workflow consists of three components:

1. **Microbiome analysis**
2. **Diet metabarcoding analysis (OBITools)**
3. **Correlation tests linking diet composition to microbiome structure**

---

## **Data Provided**

### **Raw Data (for full reproducibility)**
OBITools mithun refernce database built from ethnobiological survey from Geng et al. 2017
* `db_mithun_obitools.fasta`

### **Processed Phyloseq Objects (for easy downstream analysis)**

**`microbiome.physeq.rds`**
Filtered microbiome phyloseq object containing ASV table, taxonomy, metadata, and representative sequences.

  * `physeq.raw.rds`
  * `physeq.rare.rds`
  * `physeq_filtered.rds

**`diet.physeq.rds`**
 Phyloseq object derived from OBITools output, containing OTU table, plant taxonomy, rep-seqs (if applicable), and metadata.
  * `diet.physeq.full.rds`
  * `diet.physeq.filtered.rds`
  * `diet.physeq.rare.rds`

Users may reproduce the full pipeline from raw data or directly load these `.rds` files.

---

## **1. Microbiome Analysis**

### **Processing Steps**

1. Import phyloseq object
5. Perform **CLR transformation**.
6. Compute **Aitchison distances** (Euclidean distance of CLR-transformed data).
7. Ordinate samples using **PCoA**.
8. Visulize

---

## **2. Diet Metabarcoding Analysis (OBITools Input)**

### **Processing Steps**

1. Import Phyloseq Object
2. Perform zero replacement and apply **CLR transformation**.
3. Compute **Aitchison distances**.
4. Generate PCoA ordinations.
5. Visualize

---

## **3. Correlation Between Diet and Microbiome**

### **Steps**

1. Match sample IDs across `diet.physeq.rds` and `microbiome.physeq.rds`.
2. Subset both phyloseq objects to shared samples.
3. Compute Aitchison distance matrices for both datasets.
4. Perform multivariate correlation analyses:
   * **Mantel test** (Spearman, 999 permutations)
   * **Procrustes rotation** and **PROTEST permutation test** (999 permutations)
5. Visualize diet vs. microbiome distance relationships using scatterplots.
6. Export Mantel statistics, Procrustes statistics, and all distance matrices.

---

## **Software Requirements**
## Package versions

| Package             | Version |
|---------------------|---------|
| phyloseq            | 1.54.2  |
| microbiome          | 1.32.0  |
| microbiomeutilities | 1.00.17 |
| microViz            | 0.13.0  |
| ANCOMBC             | 2.13.1  |
| vegan               | 2.7-3   |
| permute             | 0.9-10  |
| pairwiseAdonis      | 0.4.1   |
| nlme                | 3.1-169 |
| lmerTest            | 3.1-3   |
| emmeans             | 2.0.2   |
| car                 | 3.1-5   |
| multcomp            | 1.4-30  |
| tidyverse           | 2.0.0   |
| dplyr               | 1.2.0   |
| stringr             | 1.6.0   |
| Biostrings          | 2.78.0  |
| ggplot2             | 4.0.2   |
| ggpubr              | 0.6.3   |
| patchwork           | 1.3.2   |
| RColorBrewer        | 1.1-3   |
| forcats             | 1.0.1   |
| scales              | 1.5.0   |
| grid                | 4.5.3   |

---

## **Scripts**

The repository includes three primary analysis scripts:

* `01_microbiome_analysis.R`
* `02_diet_analysis.R`
* `03_correlation_tests.R`

