# NGS Course, Session 1: Introduction to Galaxy and NGS Data Structures

# Updates

 - Please post the errors or questions on the **issue** tab on Github. This will make a record regarding solution and errors.
 - Still you could send us an email.

# Aim of course
 - We will use **Galaxy**
 - Allow you to go from raw data to analysis
 - Teach the steps and associated tools for analysis pipeline
 - Independent to work with NGS datasets
 - Develop Galaxy workflows for new analysis and pipeline : **automation**
 - Analysis of bulk RNA-seq and bulk ATAC-seq from Illumina platform

# File type and procession in NGS dataset

## Raw data

 1. fastq format : fastq format with quality scores
  - Composed of header and sequence
  - Few giga-bytes of files

 2. Trimming of fastq based on the quality
  - To trim out the regions which have low quality
  - K-mers : lack of complexity after trimming due to the lack of adapter info
  - Average of length will be changed and some could be shorter than sequenced length

## Mapping to the genome
 - Using HISAT2 : put trimmed fastq files
 - Reference genome : **Have to use UCSC, built-in genome** because galaxy is connected to UCSC. **The genome and transcriptome information from UCSC and Ensembl are totally different**!!
  - Already the genome index is included in Galaxy.

 1. SAM format : Sequence Alignment and Map information
  - Human readable : Plain text file including sequence info, quality score and *alignment information* with meta-data
  - Typically much larger size compared to original fastq file
 2. BAM format : Compressed SAM file
  - Not human readable : binary format
  - 1/5 size of SAM : easier to store

 - Those aligned reads could be converted as **custom track** on **UCSC genome browser**. The intensity of peaks on the custom track corresponds to the number of reads covering certain region.
  - If it is RNA-seq, what we could expect is that the reads will be mapped on exome regions.

## Counting
 - Still we could not know how many of reads are mapped on the certain region.
 - **htseq-count** tool is mainly used for quantification of gene expression on RNA-seq. (BAM and GFF files are required)
  - Recommend to check the parameters!!

 1. gff3 / gft format
  - Information of genome : including genomic coordinate, score, attributes..
  - **Be aware of the format being used and its compatibility!**
    - Ensembl GTF != UCSC GTF
    - Each version of genome has its specific gtf files.
  - On UCSC genome browser: Downloads > Genome Data > select species > Genome sequence files and select annnotations > refGene.gtf.gz
