6. Trimming Fastq Sequences
===========================

1. Trimming sequences

.. note :: Some sequencing run will yield poor quality data. It's best not to use it in alignment process. So we are going to trim these sequences based on quality, length, N's etc. 


::
	
	module load GNU/4.4.5
	module load sickle/1.210
	
Now copy the code below and paste 

How do you select these modules? 
	
::

	sickle
	
Now what is happening? What does your screen say or complain?

Now paste or type this (be careful with space)

::

	sickle pe -help
	

1. Follow, the format below to input in the details 

sickle pe -c <combined input file> -t <quality type> -m <combined trimmed output> -s <trimmed singles file>

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


Let's see if the file was made? 

type 

::


	ls-l

If you want to see what's in the log files, 

:: 

	nano salivary_repl1.log
	


So what do you see?





To go out of press, control X



Moving on, to save some space on the machine we are going to gzip the two files



gzip name_of _file > name_of_file.gz


-Pay attention to the .gz ending
		

::		

	gzip salivary_repl1_R1_trimmed.fq > salivary_repl1_R1_trimmed.fq.gz
	
	
	
Now try to gzip the R2 file.

