9. Count reads with HtSeq
========================
1. Now we need to count the number of reads that mapped to each gene from the tophat alignment



So, load the modules PySAM and HTSeq 

::

	module load PySAM/0.6
	module load HTSeq/0.6.1
	
	
	

If you get a message, ignore it

First check to see if you are in the tophat folder. If you are not then use cd to navigate to the directory. 


Once in the directory, now run HTSeq to get the counts

::

	htseq-count --format=bam --stranded=no --order=pos \
    accepted_hits.bam \
    ~/RNAseq-model/Homo_sapiens/Ensembl/GRCh37/Annotation/Genes/genes.gtf > salivary_repl1_counts.txt
    
    
    
Now lets see if the file is made

::

	ls -l


Lets see what the output was


::

	less salivary_repl1_counts.txt

So you can see two columns. With the first column the indicates gene name and the second column indicates the counts


use "q" to exit





