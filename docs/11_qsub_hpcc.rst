11. Submitting a Batch Job to the HPCC
===================================


The limitation of using one of the interactive nodes is 2-4 hrs. If we have jobs >4 hrs, how do we run these jobs.

The HPCC has a job submission protocol called qsub

.. note:: https://wiki.hpcc.msu.edu/display/hpccdocs/Scheduling+Jobs

::

	cat > hpcc_trial.qsub <<EOF
	
and then paste the following in:

::
	
	#! /bin/bash
	
	#PBS -o /mnt/home/perumbak/rnaseq
	#PBS -l nodes=1:ppn=2,walltime=48:00:00
	#PBS -l mem=20gb

	module load GNU/4.4.5
	module load sickle/1.210
	module load TopHat2/2.0.12
	module load PySAM/0.6
	module load HTSeq/0.6.1

	# go to the 'rnaseq' directory in my home directory
	cd ~/rnaseq

	# subset the data sets (50,000 reads) - you don't want to do this
	# on real data :)
	head -50000 ~/RNAseq-model/data/ERR315326_1.fastq | gzip > lung_repl1_R1.fq.gz
	head -50000 ~/RNAseq-model/data/ERR315326_2.fastq | gzip > lung_repl1_R2.fq.gz

	# run Sickle.  Here, the inputs are 'lung_repl1_R1.fq.gz' and
	# 'lung_repl1_R2.fq.gz', and the outputs are 'lung_repl1_R1_trimmed.fq'
	# and 'lung_repl1_R2_trimmed.fq'.
	
	sickle pe -f lung_repl1_R1.fq.gz \
              -r lung_repl1_R2.fq.gz \
              -t sanger \
              -o lung_repl1_R1_trimmed.fq \
              -p lung_repl1_R2_trimmed.fq \
              -s lung_repl1_R2_single.fq \
              -n -q20 -l50 > lung_repl1.log
                  
    	#now gzip the file so compactness
    
    	gzip lung_repl1_R1_trimmed.fq > lung_repl1_R1_trimmed.fq.gz
    	gzip lung_repl1_R2_trimmed.fq > lung_repl1_R2_trimmed.fq.gz
    
	# now run Tophat!
	# The inputs are the outputs of the previous qzip step.
	# The outputs are going to be under the 'tophat_lung_repl1' directory.
	
	tophat -G ~/RNAseq-model/Homo_sapiens/Ensembl/GRCh37/Annotation/Genes/genes.gtf \
    		--transcriptome-index=$HOME/RNAseq-model/transcriptome \
    		-o tophat_lung_repl1 \
    		~/RNAseq-model/Homo_sapiens/Ensembl/GRCh37/Sequence/Bowtie2Index/genome \
    		lung_repl1_R1_trimmed.fq.gz lung_repl1_R2_trimmed.fq.gz

	# count the hits by gene -- 'tophat_lung_repl1' is the main output,
	# from Tophat.
	htseq-count --format=bam --stranded=no --order=pos tophat_lung_repl1/accepted_hits.bam \
   	 ~/RNAseq-model/Homo_sapiens/Ensembl/GRCh37/Annotation/Genes/genes.gtf > lung_repl1_counts.txt
	EOF

Things to know:

There are many ways this can be done. You could put in all your samples and run one script or break them down so you have many scripts. The maximun time a job can be scheduled is 5 days. 


