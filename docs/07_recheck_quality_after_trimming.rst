7. Check Quality Post Trimming
============================

1. Need to check the results of trimming.


List all the files in your directory


::

	ls

.. Note :: If the fastqc module is loaded, you dont have to reload them again. If not use the command below
	
::

	module load FastQC/0.11.2
	

Now run the files ...

::


	fastqc salivary_repl1_R1_trimmed.fq.gz
	fastqc salivary_repl1_R2_trimmed.fq.gz
	
	
Now you will have two html files. Use Filezila to transfer and view these files



So how do this file compare to the pervious file?



