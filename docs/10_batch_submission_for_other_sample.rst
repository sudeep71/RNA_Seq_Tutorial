10. Processing Next Sample Through Automated Pipeline to get counts
===============================================================


We are going to repeat all this process one more time to get expression data from another set of samples.

But what we are going to do is write a script to do it (how exciting !!!!)


::

	cd ~/rnaseq/
	cat > sample_lung_tophat.sh <<EOF
	
	
Now paste this into the file:

::

	module load GNU/4.4.5
	module load sickle/1.210
	module load TopHat2/2.0.12
	module load PySAM/0.6
	module load HTSeq/0.6.1

	# go to the 'rnaseq' directory in my home directory
	cd ~/rnaseq

	# subset the data sets (100,000 reads) - you don't want to do this
	# on real data :)
	head -50000 ~/RNAseq-model/data/ERR315326_1.fastq | gzip > lung_repl1_R1.fq.gz
	head -50000 ~/RNAseq-model/data/ERR315326_2.fastq | gzip > lung_repl1_R2.fq.gz

	# run Sickle.  Here, the inputs are 'lung_repl1_R1.fq.gz' and
	# 'lung_repl1_R2.fq.gz', and the outputs are 'lung_repl1_R1_trimmed.fq'
	# and 'lung_repl1_R2.qc.fq'.
	sickle pe -f lung_repl1_R1.fq.gz \
              -r lung_repl1_R2.fq.gz \
              -t sanger \
              -o lung_repl1_R1_trimmed.fq \
              -p lung_repl1_R2_trimmed.fq \
              -s lung_repl1_R2_single.fq \
              -n -q20 -l50 > lung_repl1.log
                  
    #now gzip the file so compactness
    
    gzip lung_repl1_R1_trimmed.fq > lung_repl1_R1_trimmed.fq.qz
    gzip lung_repl1_R2_trimmed.fq > lung_repl1_R2_trimmed.fq.qz
    
	# now run Tophat!
	# The inputs are the outputs of the previous qzip step.
	# The outputs are going to be under the 'tophat_lung_repl1' directory.
	tophat -p 4 \
    	-G ~/RNAseq-model/Homo_sapiens/Ensembl/GRCh37/Annotation/Genes/genes.gtf \
    	--transcriptome-index=$HOME/RNAseq-model/transcriptome \
    	-o tophat_lung_repl1 \
    	~/RNAseq-model/Homo_sapiens/Ensembl/GRCh37/Sequence/Bowtie2Index/genome \
    	lung_repl1_R1_trimmed.fq.qz lung_repl1_R2_trimmed.fq.qz

	# count the hits by gene -- 'tophat_lung_repl1' is the main output,
	# from Tophat.
	htseq-count --format=bam --stranded=no --order=pos tophat_lung_repl1/accepted_hits.bam \
   	 ~/RNAseq-model/Homo_sapiens/Ensembl/GRCh37/Annotation/Genes/genes.gtf > lung_repl1_counts.txt
	EOF


.. note:: "#" or hash can be use in scripting language and the machine is inbuilt to leave or ignore these lines. So you can use # to be explicit. 

You can use "nano" to edit the file

::

	nano sample_lung_tophat.sh


::

	bash sample_lung_tophat.sh
	
	
