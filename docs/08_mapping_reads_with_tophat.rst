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
    


What does all this mean?


Will take ~20 min to finish


Now what are these parameters?


For more information check the tophat manual (http://ccb.jhu.edu/software/tophat/manual.shtml)

2. Now once the alingment is done look up the statistics


What has happened? How many pairs of reads were present and how many aligned?




