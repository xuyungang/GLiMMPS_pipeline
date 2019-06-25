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
## 2. Data download and processing (Geuvadis as example)
### 2.1 RNA-seq data download
**(1) Download metadata** (sample list): Go to Geuvadis [Dataport](http://www.internationalgenome.org/data-portal/data-collection/geuvadis), select the *Data types* as `Sequence` and the *Analysis groups* as `mRNA`, and then click `Download the list` button to get the metadata (*igsr_Geuvadis.tsv.tsv*) of all five Geuvadis populations (CEU, FIN, GBR, TSI, and YRI).

**(2) Batch download**: use `fastqDownloader.sh` to downlaod the samples you need. Take CEU population as example, first take out those lines for CEU from *igsr_Geuvadis.tsv.tsv*, you can run `grep "CEU" igsr_Geuvadis.tsv.tsv >> CEU_igsr_Geuvadis.tsv.tsv`; then run `bash fastqDownloader.sh CEU_igsr_Geuvadis.tsv.tsv 50` to download the fastq files for samples included in **CEU_igsr_Geuvadis.tsv.tsv** with 50 threads parallelly.
fastq files will be downloaded and grouped into different folders named as the population ID, like CEU etc. All fastq files will also be renamed as <Idividual_ID>\_<Sample_ID>\_1.fastq.gz, like NA06984_ERR188325_1.fastq.gz.
### 2.2 QC and alignment
**(1) QC**: we ran trim_galor on the pairwise fastq files (set --paired) to make sure all reads have the same length of 75bp; and then run fastqc for QC filtering.

**(2) Merge replicates for single individual**: after trim and QC, many of the idviduals will have more than one replicates, we merged the fastq files of replicates, so that each individual will have only one pair fastq files, named as <Individual_ID>\_1.fq.gz and <Individual_ID>\_2.fq.gz. In total, for CEU population, there will be 184 fastq files for 92 individuals.

**(3) Alignment using STAR**: run `mapSTAR.sh <Individual_ID>` to map the reads to hg19 genome and get the uniquely mapped reads. The unique.sam files will be in *sam_unique/* with the subfolder named with the <Individual_ID>.
## 3. Run GLiMMPs pipeline
### 3.1 Obtai the junction read counts for all possible alternative splicing events in the population
**(1) Get all possible alternative splicing (AS) events in the population.**

Customize the config.GLiMMPS.txt for the population, which contains main parapeters for all data processing.

  ```/GLiMMPscode/pythonperlsrcs/batch_allASevents.pl /GLiMMPscode/config.GLiMMPS.txt```
  
  
