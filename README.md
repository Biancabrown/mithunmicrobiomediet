# mithunmicrobiomediet

# **README**

## **Overview**

This repository contains the code and data used to process and analyze the rumen microbiome and diet metabarcoding datasets for the mithun (*Bos frontalis*) seasonal ecology study.

To support reproducibility **and** facilitate downstream analysis, the repository includes:

* **Raw input files** (QIIME2 artifacts, OBITools output, and metadata)
* **Processed R objects**:

  * `microbiome.physeq.rds`
  * `diet.physeq.rds`

These `.rds` files contain fully assembled and filtered **phyloseq objects** that can be loaded directly for ordination, distance calculations, and correlation testing.

The workflow consists of three components:

1. **Microbiome analysis**
2. **Diet metabarcoding analysis (OBITools)**
3. **Correlation tests linking diet composition to microbiome structure**

---

## **Data Provided**

### **Raw Data (for full reproducibility)**

**Microbiome (QIIME2):**

* `table.qza` – ASV/feature table
* `taxonomy.qza` – taxonomy assignments
* `rep-seqs.qza` – representative sequences
* `sample-metadata.tsv` – microbiome metadata

**Diet (OBITools):**

* `obitools.output.txt` – OBITools plant metabarcoding table (samples × taxa with assigned taxonomy)
* `mithun.samples.txt` – diet sample metadata

### **Processed Phyloseq Objects (for easy downstream analysis)**

**`microbiome.physeq.rds`**
Filtered microbiome phyloseq object containing ASV table, taxonomy, metadata, and representative sequences.

**`diet.physeq.rds`**
Filtered diet phyloseq object derived from OBITools output, containing OTU table, plant taxonomy, rep-seqs (if applicable), and metadata.

Users may reproduce the full pipeline from raw data or directly load these `.rds` files.

---

## **1. Microbiome Analysis**

### **Processing Steps**

1. Import QIIME2 files using `qiime2R`.
2. Construct a phyloseq object.
3. Remove non-bacterial contaminants (mitochondria, chloroplast, unassigned).
4. Remove singletons (taxa with total count ≤ 1).
5. Perform zero replacement and apply **CLR transformation**.
6. Compute **Aitchison distances** (Euclidean distance of CLR-transformed data).
7. Ordinate samples using **PCoA**.
8. Save final processed object as `microbiome.physeq.rds`.

---

## **2. Diet Metabarcoding Analysis (OBITools Input)**

### **Processing Steps**

1. Import OBITools output (`obitools.output.txt`), containing:

   * sample columns (`sample.*`)
   * OTU/sequence IDs
   * OBITools taxonomy annotations
2. Construct a phyloseq OTU table from sample columns.
3. Construct a phyloseq taxonomy table from taxonomic columns
   (order, family, genus, species).
4. Import sample metadata (`mithun.samples.txt`) and add to the phyloseq object.
5. Remove rare plant taxa and singletons.
6. Perform zero replacement and apply **CLR transformation**.
7. Compute **Aitchison distances**.
8. Generate PCoA ordinations.
9. Save final processed object as `diet.physeq.rds`.

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

* **R ≥ 4.0**
* Required packages:

  * `phyloseq`
  * `qiime2R`
  * `tidyverse`
  * `vegan`
  * `microbiomeutilities`
  * `stringr`
  * `compositions`

---

## **Scripts**

The repository includes three primary analysis scripts:

* `01_microbiome_analysis.R`
* `02_diet_analysis.R`
* `03_correlation_tests.R`

