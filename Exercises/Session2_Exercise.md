Assignment, Session 2: Generate an automated pipeline for DGE using Galaxy Dataset List
================

In this exercise, you will automate the RNA-Seq. pipeline using Galaxy Datasets.

Step 1: Get the data to Galaxy
------------

Upload the raw data from Session 2 Preparation to Galaxy. Upload via FTP client.  

Also, upload the [zebrafish transcriptome file downloaded from UCSC](http://hgdownload.soe.ucsc.edu/goldenPath/danRer11/bigZips/genes/)

Step 2: Generate a collection
----------

1. Click on the tick mark in the History panel that says 'Operations on multiple datasets' and select all the raw data files (Select 'All', and remove the selection from gtf file).

![Tick](https://github.com/sumeetpalsingh/NGS_Course/blob/master/images/Tick.png)

2. Click on 'For all selected', and choose the option 'Build Lists of Dataset Pairs'

3. In the new pop-up window you will see that the files are incorrectly paired. Click on 'unpair all' to remove the pairing.

4. Relace '_1' and '_2' with '_R1' and '_R2'. These define the pairing between raw data files. Press 'Auto Pair'.

5. At the bottom, enter the name of the collection (Example:'Experiment'), and 'Create list'.

Step 3: Mapping
----------

Run Hisat2 with the following parameters.
1. Reference Genome: Zebrafish May 2017 (GRCz11 / danRer11) danRer11
2. Is this a single or paired library: Paired end dataset collection
3. Paired Collection: Experiment
4. Summary options: Print alignment summary to a file.: 'Yes'
5. Advanced options:
  + Scoring options: Specify Scoring options.
    + Allow soft-clipping: Yes
  + Spliced alignment options: Specify Spliced alignment options
    + GTF file with known splice sites: danRer11.refGene.gtf.gz (your chosen gtf file from UCSC)

Step 4: Read counting
--------



Good luck
