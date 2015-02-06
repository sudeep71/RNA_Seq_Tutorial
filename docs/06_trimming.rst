6. Trimming Fastq Sequences
===========================

1. Trimming sequences

.. note :: Some sequencing run will yield poor quality data. It's best not to use it in alignment process as it will lead to spurious results. So we are going to trim these sequences based on quality, length, N's etc. 

Now copy the code below and paste 

::
	
	module load GNU/4.4.5
	module load sickle/1.210
	

How do you select these modules? 
	
::

	sickle
	
Now what is happening? What does your screen say or complain?

Now paste or type this (be careful with space)

::

	sickle pe -help
	

1. Follow, the format below to input in the details 

sickle pe -c <combined input file> -t <quality type> -m <combined trimmed output> -s <trimmed singles file>

The below command can either be pasted as as single line or the by the format shown below


::


	sickle pe -f salivary_repl1_R1.fq.gz \
		-r salivary_repl1_R2.fq.gz \
		-t sanger \
		-o salivary_repl1_R1_trimmed.fq \
		-p salivary_repl1_R2_trimmed.fq \
		-s salivary_trimmed_single.fq \
		-n -q20 -l50 > salivary_repl1.log

Where:

-q, --qual-threshold, Threshold for trimming based on average quality in a window. Default 20

-l, --length-threshold, Threshold to keep a read based on length after trimming. Default 20

-n, --discard-n, Discard sequences with any Ns in them

-s, orphan reads that do not from pairs

-l, length of read


Let's see if the files were made? 

type 

::


	ls-l

If you want to see what's in the log files, 

:: 

	nano salivary_repl1.log
	


So what do you see?





To close nano, press control x



Moving on, to save some space on the machine we are going to gzip the two files



gzip name_of _file > name_of_file.gz


- Pay attention to the .gz ending
		

::		

	gzip salivary_repl1_R1_trimmed.fq > salivary_repl1_R1_trimmed.fq.gz
	
	
	
Now try to gzip the trimmed R2 file.

