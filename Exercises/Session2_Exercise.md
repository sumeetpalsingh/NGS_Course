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

![Tick](https://github.com/sumeetpalsingh/NGS_Course/blob/master/images/exercise2/Tick.png)

2. Click on 'For all selected', and choose the option 'Build Lists of Dataset Pairs'

![Build](https://github.com/sumeetpalsingh/NGS_Course/blob/master/images/exercise2/BuildList.png)

3. In the new pop-up window you will see that the files are incorrectly paired. Click on 'unpair all' to remove the pairing.

![WrongPair](https://github.com/sumeetpalsingh/NGS_Course/blob/master/images/exercise2/WrongPair.png)

4. Relace '_1' and '_2' with '_R1' and '_R2'. These define the pairing between raw data files. Press 'Auto Pair'.

![CorrectPair](https://github.com/sumeetpalsingh/NGS_Course/blob/master/images/exercise2/CorrectPair.png)

5. At the bottom, enter the name of the collection (Example:'Experiment'), and 'Create list'.

![Name](https://github.com/sumeetpalsingh/NGS_Course/blob/master/images/exercise2/Name.png)

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

Run htseq-count with the following parameters.
1. Aligned SAM/BAM File: Dataset Collection
  + HISAT2 on collection: aligned reads (BAM)
2. GFF file: danRer11.refGene.gtf.gz
3. Stranded: 'No'

![Count](https://github.com/sumeetpalsingh/NGS_Course/blob/master/images/exercise2/Count.png)

Step 5: Generate count matrix
-------

Generate a single file with all the counts aggregated
1. In the Tools panel, select '**Join, Subtract and Group**'. Choose '**Column Join** on Collections'

![Join](https://github.com/sumeetpalsingh/NGS_Course/blob/master/images/exercise2/Join.png)

2. Select '**Tabular files**': 'Dataset collections': 'htseq-count on collection'

![Tabular](https://github.com/sumeetpalsingh/NGS_Course/blob/master/images/exercise2/Tabular.png)

3. You will get a single count table with counts from all datasets.

![matrix](https://github.com/sumeetpalsingh/NGS_Course/blob/master/images/exercise2/matrix.png)

4. Click on the eye button 'View data' to view the matrix

![matrix2](https://github.com/sumeetpalsingh/NGS_Course/blob/master/images/exercise2/matrix2.png)

Step 6: Differential Gene Expression (DGE) Analysis
--------

For DGE we will use EdgeR. Search for 'edgeR' in tool panel and select the tool.

![edgeR](https://github.com/sumeetpalsingh/NGS_Course/blob/master/images/exercise2/edgeR.png)

Run the tool with following parameters:

1. **Count Files or Matrix?**: Single Count Matrix
2. **Count Matrix**: Column Join on data ..
![input](https://github.com/sumeetpalsingh/NGS_Course/blob/master/images/exercise2/input.png)
3. Factor
  + 1: Factor (Here we define the contrast that we are interested in)
    + **Factor Name**: Treatment
    + **Groups**: Treat,Control,Control,Treat (NOTE: the order of groups should match your count matrix!!!)

![factor](https://github.com/sumeetpalsingh/NGS_Course/blob/master/images/exercise2/factor.png)

4. Contrast
  + **Contrast of Interest**: Treat-Control (Should match the names of Groups mentioned above)

![contrast](https://github.com/sumeetpalsingh/NGS_Course/blob/master/images/exercise2/contrast.png)

This will give you results in html format.


Step 7: Remove Batch Effect (Self-exercise)
--------

Remove batch effects from DGE. This can be done by specifying an additional Factor level (read the **What it does** text in EdgeR tool (scroll down after selecting the tool)).

Add a second factor level after the first one (which defines the treatment)

**2: Factor** (Here we define the contrast we are **not** interested in)
  + **Factor Name**: Batch
  + **Groups**: Batch2,Batch1,Batch2,Batch1 (NOTE: the order of groups should match your count matrix!!!)

![factor2](https://github.com/sumeetpalsingh/NGS_Course/blob/master/images/exercise2/factor2.png)

Good luck!
