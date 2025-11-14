# WES Variant Analysis for Triple Negative Breast Cancer (TNBC)

This repository contains the complete bioinformatics analysis, from raw data to prioritized variant lists, for a Whole Exome Sequencing (WES) sample (`SRR34853843`).

This project demonstrates an end-to-end workflow to identify significant genetic variants in a Triple Negative Breast Cancer sample from a South Asian cohort, a population historically underrepresented in genomic research.

---

## 1. Project Overview

### 🧬 About the Data

The raw sequencing data was obtained from the public Sequence Read Archive (SRA).

* **Study:** PRJNA1298555
* **Sample:** SAMN50279194
* **Run ID:** SRR34853843
* **Strategy:** Whole Exome Sequencing (WXS)
* **Instrument:** Illumina NovaSeq X

**Study Abstract (Paraphrased):**
> TNBC is a genetically heterogeneous disease with diverse mutational profiles across different ethnicities. This study aims to address the significant gap in knowledge for South Asian populations, seeking to identify clinically actionable genetic variants for potential therapeutic intervention.

---

## 2. Methodology & Pipeline

This analysis involved a standard bioinformatics pipeline to process raw FASTQ reads, identify variants, and annotate their functional impact.

1.  **Quality Control (QC):**
    * Raw paired-end reads (`.fastq`) were assessed using **FastQC** to check for base quality, adapter content, and duplication levels.

2.  **Alignment & Post-Processing:**
    * Reads were aligned to the human reference genome (GRCh38).
    * The resulting `.bam` file was sorted and indexed using **Samtools**.
    * PCR duplicates, a common artifact in WES, were identified and marked using **Picard MarkDuplicates**.

3.  **Variant Calling:**
    * Variants (SNPs and Indels) were called from the processed `.bam` file to generate a `.vcf` file.

4.  **Variant Annotation:**
    * The raw `.vcf` file was annotated using **SnpEff** to predict the functional consequences of each variant (e.g., missense, frameshift, stop-gained).

5.  **Filtering & Prioritization:**
    * The annotated VCF was filtered to isolate the most significant findings. The final results are summarized in the `.tsv` files, focusing on high and moderate-impact variants.

---

## 3. Key Analytical Findings

The pipeline successfully processed and annotated **815,355** total variants. Filtering these for functional significance revealed several key findings:

### High-Impact Variants
A set of disruptive variants (frameshift, stop-gained, and splice-site mutations) were identified. These variants are most likely to result in non-functional proteins and are prime candidates for further investigation.

Key genes with high-impact variants included:
* `NPHP4` (splice acceptor variant)
* `CAMTA1` (start lost)
* `PER3` (frameshift variant)
* `KIF1B` (frameshift variant)
* `TARDBP` (stop gained)
* `ALK` (stop gained)
* `FCGBP` (frameshift variant)

### Moderate-Impact (Missense) Variants
A large number of missense variants (which change a single amino acid) were identified. Notable findings include:
* **MTHFR:** A `p.Ala222Val` missense variant was identified. This is a very common and well-studied polymorphism related to folate metabolism.
* **HLA-A:** Multiple missense variants were found, which is expected given the high variability of HLA genes critical for immune function.
* **MUC16:** Numerous missense variants were identified in this gene, which codes for the CA-125 cancer antigen.

---

## 4. Repository Contents

This repository contains the primary output files from the analysis pipeline.

* `/fastqc/`:
    * `SRR34853843_1_fastqc.html`: FastQC report for Read 1.
    * `SRR34853843_2_fastqc.html`: FastQC report for Read 2.
* `/metrics/`:
    * `metrics.txt`: Duplication metrics output from Picard MarkDuplicates.
* `/annotation/`:
    * `snpEff_summary.html`: SnpEff summary report, detailing variant types and impacts.
    * `snpEff_genes.txt`: A gene-by-gene breakdown of variant effects.
* `/results/`:
    * `high_moderate_variants.tsv`: A filtered list of all high and moderate-impact variants.
    * `filtered_main_variants.tsv`: A filtered list for key findings.
    * `main_findings.tsv`: A summarized table of the most significant variants.

---

## 5. License

This project is licensed under the MIT License.
