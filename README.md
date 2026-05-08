# mithunmicrobiomediet

# **README**

Signatures of the wild: Seasonal variation of microbiome and diet in the mountain roaming semi-domesticated mithun, Bos frontalis 
Yanfei Geng1,2,3,#, Bianca R. P. Brown4,#, Shengtao Gao1,5,6, Qiaoshun Yan7,8,9,10, Lu Ma1,11, Jianchu Xu1,3,11*, Dengpan Bu1,11*

1State Key Laboratory of Animal Nutrition and Feeding, Institute of Animal Science, Chinese Academy of Agricultural Sciences, Beijing 100193, China
2College of Life Sciences, Guizhou University, Guiyang 550025, China
3Key Laboratory of Economic Plants and Biotechnology, Kunming Institute of Botany, Chinese Academy of Sciences, Kunming 650201, China
4Yale University, Department of Molecular Biophysics and Biochemistry, New Haven, CT, USA
5College of Life Sciences and Technology, Inner Mongolia Normal University, Hohhot, Inner Mongolia, 010018, China
6Key Laboratory of Biodiversity Conservation and Sustainable Utilization in Mongolian Plateau for College and University of Inner Mongolia Autonomous Region, Hohhot, 010018, China
7Yunnan Key Laboratory of Forest Ecosystem Stability and Global Change, Xishuangbanna Tropical Botanical Garden, Chinese Academy of Sciences, Mengla, Yunnan, 666303, China
8Ailaoshan Station of Subtropical Forest Ecosystem Studies, Xishuangbanna Tropical Botanical Garden, Chinese Academy of Sciences, Jingdong, Yunnan, 676209, China
9 University of Chinese Academy of Sciences, Beijing 100049, China
10Ailaoshan Subtropical Forest Ecosystem Observation and Research Station of Yunnan Province，Jingdong, Yunnan, 676209, China
11CAAS-ICRAF Joint Lab on Agroforestry and Sustainable Animal Husbandry, World Agroforestry Centre, East and Central Asia, Beijing 100193, China


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

### **01.microbiome_analysis.Rmd**
1. Alpha Diversity
2. Perform **CLR transformation**.
3. Compute **Aitchison distances** (Euclidean distance of CLR-transformed data).
4. Ordinate samples using **PCoA**.
5. Visulize
6. Statistical test -- ANOVA, PERMANOVA, ANCOMBC-2
---

## **2. Diet Metabarcoding Analysis (OBITools Input)**

### **02.diet_analysis.Rmd**

1. Alpha Diversity
2. Perform **CLR transformation**.
3. Compute **Aitchison distances** (Euclidean distance of CLR-transformed data).
4. Ordinate samples using **PCoA**.
5. Visulize
6. Statistical test -- ANOVA, PERMANOVA
---

## **3. Correlation Between Diet and Microbiome**

### **03.microbiome-diet-correlation**

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

