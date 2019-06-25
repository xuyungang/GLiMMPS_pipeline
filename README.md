# GLiMMPs_pipeline
This repository contains the source codes of the pipeline for sQTL mapping and illustrates the usage by performing an example on the data of Gevadis CEU population.
## 1. Prerequisites
The full pipeline starts with data download and ends with sQTL mapping using GLiMMPs, which requires all tools for fastq files download, quality control (QC), alignment, vcf manipulate tools, and running environments for GLiMMPs (Python, Per, and R).
### 1.1 Download and install RNA-seq reads alignment tool 'STAR' (version 2.6.1)
Refer to STAR GitHub page for instructions: https://github.com/alexdobin/STAR
### 1.2 Download and install BAM file tool 'samtools'
