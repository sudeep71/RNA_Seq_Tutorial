Obtaining Data and Read Quality 
================================

The data we will be using has been downloaded from the source. You will not be doing this part.

Two samples: salivary gland and lung. Note that each sample has one replicates, and each replicate has two files.

.. note:: Since downloading this data takes hours, the data has been already downloaded and put into a folder for connivence

.. note:: The command line is case sensitive. So be careful when to type commands. The best practice is to use lower case, underscore (_), and no spaces between words eg. course_work_project_mmg433. Also try to be as explicit in naming folders or use a data stamp eg. mmg443_rnaseq_tutorial_1/1/2015. 


 1. Lets start the process by first logging on to the HPCC


Now that you are logged  into the HPC with SSH; use your MSU NetID and log into the machine ‘gateway.hpcc.msu.edu’. 

::

	module load powertools
	getexample RNAseq-model
	
.. note:: This loads the data from the machine to your home folder

Now log into a node:

::

	ssh dev-intel14-phi
	
Once you log into the dev node, type or paste the following 

::

	ls -la ~/RNAseq-model/data/
	
This is what you will see (a list of all files with size and owner)

::

	-r--r--r-- 1 mscholz common-data 3714262571 Dec  4 08:44 ERR315325_1.fastq
	-r--r--r-- 1 mscholz common-data 3714262571 Dec  4 08:44 ERR315325_2.fastq
	-r--r--r-- 1 mscholz common-data 2365633645 Dec  4 08:44 ERR315326_1.fastq
	-r--r--r-- 1 mscholz common-data 2365633645 Dec  4 08:44 ERR315326_2.fastq


Now we have to copy this data to your home directory


2. Copying the original data to your folder by first making a directory:

::

	mkdir ~/rnaseq 
	cd ~/rnaseq

Now we are not going to work with the complete dataset, just a small fraction (50,000 reads):

::

	head -50000 ~/RNAseq-model/data/ERR315325_1.fastq | gzip > salivary_repl1_R1.fq.gz 
	head -50000 ~/RNAseq-model/data/ERR315325_2.fastq | gzip > salivary_repl1_R2.fq.gz


.. note:: What are above commands doing? First of all there are 2 programs being used in this process. We call head, a program which reads the top of lines of a file (1 to 10000 etc.) to read the first 50,000 lines from the file ERR315325_1.fastq. We are also giving what is called the "complete path" (~/RNAseq-model/data/ERR315325_1.fastq), which is a "good practice", when using the command line. Now the 50,000 lines from the fastq file is transfered to gzip, another program, in the pipeline. The symbol "|" is called "piped", which takes the output from one program, in our case head, and inputs to the other program, gzip. So gzip now takes the 50,000 lines and renames it salivary_repl1_R1.fq.gz and then zips (.gz extension) to reduce space.


Now we have two files, with R1 and R2 suffix. 




3. What is a fastq file?


.. note:: You do not want to open fastq files using word, excel, other programs due to corruption issues. The best is to use the terminal to open the files these big. 
.. note:: Why do you have two files for each sample?

info: http://en.wikipedia.org/wiki/FASTQ_format

.. image:: /images/getdata_readquality/fastq_fig.png


4. Examine the fastq file

::

	less salivary_repl1_R1.fq.gz
	
	
You can see the file organization 

hit "q" to quit from the screen and go back to promt.
	
4. Check quality of fastq file 

::

	module load FastQC/0.11.2

- Now run FASTQC on both the files 


::

	fastqc salivary_repl1_R1.fq.gz
	fastqc salivary_repl1_R2.fq.gz

- Now we can view the results of the analysis

- The files that were generated with the fastqc run (run ls):

::

	ls

::

	salivary_repl1_R1_fastqc.html
	salivary_repl1_R1_fastqc.zip
	salivary_repl1_R2_fastqc.html
	salivary_repl1_R2_fastqc.zip


Copy these files to your laptop. Now use Filezilla to log into your account then drag and drop to your computer and open using a bowser. 