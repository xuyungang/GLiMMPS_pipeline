# GLiMMPs_pipeline
This repository contains the source codes of the pipeline for sQTL mapping and illustrates the usage by performing an example analysis on the data of Gevadis CEU population.
## 1. Prerequisites
The full pipeline starts with data download and ends with sQTL mapping using GLiMMPs, which requires all tools for fastq files download, quality control (QC), alignment, vcf manipulate tools, and running environments for GLiMMPs (Python, Per, and R).
### 1.1 Download and install RNA-seq reads alignment tool `STAR` (version 2.6.1)
Refer to [STAR GitHub](https://github.com/alexdobin/STAR) page for detailed instructions.
### 1.2 Download and install BAM file tool `samtools`(version 1.9)
Refer to [samtools GitHub](https://github.com/samtools/samtools) page for detailed instructions.
### 1.3 Download and install `vcftools` (version 0.1.13)
Refer to [vcftools](https://vcftools.github.io/examples.html) page for detailed instructions.
### 1.3 Downlaod and install `plink` (version 1.07)
Refer to [plink](http://zzz.bwh.harvard.edu/plink/download.shtml) page for detailed instructions.
## 2. Data download (Geuvadis as example)
### 2.1 RNA-seq data download
.. **(1) Download metadata** (sample list): Go to Geuvadis [Dataport](http://www.internationalgenome.org/data-portal/data-collection/geuvadis), select the *Data types* as `Sequence` and the *Analysis groups* as `mRNA`, and then click `Download the list` button to get the metadata (*igsr_Geuvadis.tsv.tsv*) of all five Geuvadis populations (CEU, FIN, GBR, TSI, and YRI).
.. **(2) Batch download**: use `fastqDownloader.sh` to downlaod the samples you need. Take CEU population as example, first take out those lines for CEU from *igsr_Geuvadis.tsv.tsv*, you can run `grep \"CEU\" igsr_Geuvadis.tsv.tsv >> CEU_igsr_Geuvadis.tsv.tsv`; then run `bash fastqDownloader.sh CEU_igsr_Geuvadis.tsv.tsv 50` to download the fastq files for samples included in **CEU_igsr_Geuvadis.tsv.tsv** with 50 threads parallelly.
