# NGS Course, Session 2: RNA-Seq. Analysis

# Mapping pipeline

 - Multiple step process : both single-end and paired-ends

## Trimming - Quality control

 - Adapter trimming is **optional**
 - **Trim Galore!** could be used for trimming of adapters
  - base-pair quality < 20
  - Discard reads that became shorter than = the length of reads after trimming adapter sequences and low quality regions
 - On paired-end, *do not include the unpaired reads in the output!*

## Spice-aware mapping to genome
 - Spice-aware mapping to genome : The tool should understand that **the exons are not continuous**.
 - HISAT2 will be used for alignment
  - Input = trimmed reads
  - Spice-aware == need to tell where the exons are located
    - Reference does not have information
      - specify spice awareness option on for **Spliced alignment options**
      - Need to put the **gtf file** for making splice-aware
  - Spliced reads are joined by dashed line on IGV
    - cf. Read pairs are joined by solid line
  - **Alignment rate check required**
   - less than 30% = too less amount of material / problem while processing samples
   - Could use this as quality check between datasets
   - Above 60% is okay
   - Consistently low number == problem on sample preparation

## Counting
 - Need aligned bam files and gtf files
 - Need to check parameters
  - Stranded == no
  - Feature type == exon : the feature is belonged to exon
 - Count report : not that important
 - Count file == will be used for analysis
  - Should check whether all the values are zero == not correct
 - Put the tag == put the sample name

# Workflow
 - Automate the pipeline : do not have to find each tool

## Make Workflow
 - Could make the series of tools as a group of box
  - Considering the manipulation
  - think the flow of input and output

# Soft clipping
 - There will be a part of unmapped portion of reads
  - The reads will be separated into two seed and mapped to two exons : in case of splice-aware
  - Might have a mis-match > Ignore the mismatch and extend the maapping
  - Adapter reads or poor quality = will be kept under the soft clipping scheme
- Put the panelty on each mis-match and giving the threshold for keeping or not == giving tolerant on the trimming
- Maximum soft-clipping panelty : depend on the quality of data

# DEG analysis with DESeq2
