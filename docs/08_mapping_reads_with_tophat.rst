8. Mapping reads with Tophat2
==========================

Now we are all set, as we have good quality reads to map it to the human genome. To do this we will use a program called Tophat.



So before we start...

What are the things we need to map reads to the genome?

1) program: Tophat
2) genome sequence: Human 
3) Name of genes: GTF file or transcriptome index
4) Reads: Paired end reads

So lets start with loading the program into our workspace


1. Load the software 

::

	module load TopHat2/2.0.12
	

	
Before we run Tophat, check that we are in our working dir


::

	cd ~/rnaseq
	
:: 

	tophat -p 4 \
    -G ~/RNAseq-model/Homo_sapiens/Ensembl/GRCh37/Annotation/Genes/genes.gtf \
    --transcriptome-index=$HOME/RNAseq-model/transcriptome \
    -o tophat_salivary_repl1 \
    ~/RNAseq-model/Homo_sapiens/Ensembl/GRCh37/Sequence/Bowtie2Index/genome \
    salivary_repl1_R1_trimmed.fq.gz salivary_repl1_R2_trimmed.fq.gz
    


What does all this mean? Lets first start this command and then talk about it as it will take ~20 min to complete



Now what are these parameters?


If you want a comprehensive list of commands that are used in Tophat, check the tophat manual (http://ccb.jhu.edu/software/tophat/manual.shtml)


2. Now once the alingment is done, lets look up the statistics

So first cd into the output dir

::

	cd tophat_salivary_repl1
	
	
::

	ls
	

This list 8 files.

	
Now use nano to open the file 

::
	
	nano align_summary.txt


What has happened? How many pairs of reads were present and how many aligned?


now use Control x to close nano


So what are the files.

- What is a BAM file?


http://samtools.github.io/hts-specs/SAMv1.pdf



