Calculating Differential Expression 
====================================


We’ll be using a software package called edgeR to do the basic differential expression analysis of our counts. There are numerous methods and each has it positives and negatives.


To run edgeR, you need to write a data loading and manipulation script in R. In this case, one is provided – lung_saliva.R. 


- Running  edge R on an example data subset

::

cd ~/rnaseq
curl -O http://2014-msu-rnaseq.readthedocs.org/en/latest/_static/lung_saliva.R
curl -O http://2014-msu-rnaseq.readthedocs.org/en/latest/_static/subset/lung_repl1_counts.txt
curl -O http://2014-msu-rnaseq.readthedocs.org/en/latest/_static/subset/lung_repl2_counts.txt
curl -O http://2014-msu-rnaseq.readthedocs.org/en/latest/_static/subset/salivary_repl1_counts.txt
curl -O http://2014-msu-rnaseq.readthedocs.org/en/latest/_static/subset/salivary_repl2_counts.txt


.. note:: The saliva_repl1_counts.txt and lung_repl1_counts.txt are the files produced by mapping reads to the transcriptome with TopHat and Processing another sample with TopHat and HTSeq, respectively. The samples were run in replicate data sets, which produced the *repl2_counts.txt files.


Next, to run the R script, do:


module load R
Rscript lung_saliva.R


This will produce two files, edgeR-MA-plot.pdf and edgeR-lung-vs-salivary.csv; they will be in your rnaseq folder in your home directory on the HPC. The CSV file can be opened directly in Excel; you can also look at it here. It consists of five columns: gene name, log fold change, P-value, and FDR-adjusted P-value.


This file can then be used for pathway analysis, which will be covered in a later part of the class.