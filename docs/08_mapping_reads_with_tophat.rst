8. Mapping reads with Tophat2
==========================

Now we are all set, as we have good quality reads to map it to the human genome. To do this we will use a program called Tophat.


1. Load the software 

::

	module load TopHat2/2.0.12
	
Now to run Tophat2:

Now to check that we are in the same dir


::

	cd ~/rnaseq
	
:: 

	tophat -p 4 \
    -G ~/RNAseq-model/Homo_sapiens/Ensembl/GRCh37/Annotation/Genes/genes.gtf \
    --transcriptome-index=$HOME/RNAseq-model/transcriptome \
    -o tophat_salivary_repl1 \
    ~/RNAseq-model/Homo_sapiens/Ensembl/GRCh37/Sequence/Bowtie2Index/genome \
    salivary_repl1_R1_trimmed.fq.gz salivary_repl1_R2_trimmed.fq.gz
    


Will take ~20 min to finish


Now what are these parameters?


For more information check the tophat manual (http://ccb.jhu.edu/software/tophat/manual.shtml)

2. Now once the alingment is done look up the statistics


What has happened? How many pairs of reads were present and how many aligned?




