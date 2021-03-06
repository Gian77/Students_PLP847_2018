# Students_PLP847_2018 
Student repo bioinfo code, homework and assignments etc.

# Homework - Tuesday Oct 23rd 2018

# to reach me see below
Gian M N Benucci, Ph.D.<br/>
Michigan State University<br/>
benucciATmsu.edu

# Let's start!

Download the `homework.tar.gz` file form Github then 
Login into HPCC and then into one of the dev nodes

for example the development node intel18
`[benucci@gateway-03 ~]$ ssh dev-intel18`

in your home/ create a folder called miseq_students_2018/

`[benucci@dev-intel18 ~]$ mkdir miseq_students_2018/`

and enter inside it

`[benucci@dev-intel18 ~]$ cd miseq_students_2018/`

Upload `homework.tar.gz` into the newly created student_miseq_2018/ 
you can use command line script or Filezilla 
(recommended) to do so. Unpack it. List the content!

`[benucci@dev-intel14 miseq_students_2018]$ tar -xvzf homework.tar.gz`<br/> 
`[benucci@dev-intel14 miseq_students_2018]$ cd homework/`<br/>
`[benucci@dev-intel18 homework]$ ll`

f: this must be the last flag of the command, and the tar file must be immediately after. <br/>
   It tells tar the name and path of the compressed file.<br/>
z: tells tar to decompress the archive using gzip<br/>
x: tar can collect files or extract them. x does the latter.<br/>
v: makes tar talk a lot. Verbose output shows you all the files being extracted.<br/>

you should see something like this

`total 20`<br/>
`drwxr-x--- 2 benucci psm   3 Oct 17 21:12 raw_reads`<br/>
`-rw-r----- 1 benucci psm 443 Oct 17 21:09 README.txt`<br/>
`-rw-r----- 1 benucci psm 981 Oct 16 15:25 test.sb`

explore the folder and files using `cd, ll, ls, cat, head, tail` ...
if you need help on how to use a command use `man <commandname>` or
 `<commandname> --help`,  for example

`[benucci@dev-intel18 homework]$ ll --help`

Now you are ready to test the environment and see if you can perform
some analyses into your HPCC account. Look at the script called `test.sb` 

`[benucci@dev-intel18 homework]$ cat test.sb`

You will print something like this

------------- start code ---------------<br/>
`#!/bin/bash -login`<br/>

`#SBATCH --time=00:10:00			# limit of wall clock time - how long the job will run (same as -t)`<br/>
`#SBATCH --ntasks=1			# number of tasks - how many tasks (nodes) that you require (same as -n)`<br/>
`#SBATCH --cpus-per-task=4		# number of CPUs (or cores) per task (same as -c)`<br/>
`#SBATCH --mem=2G			# memory required per node - amount of memory (in bytes)`<br/>
`#SBATCH --job-name prefilteringQC	# you can give your job a name for easier identification (same as -J)`<br/>
 
`module load powertools			# load necesary modules`<br/>

`cd ${SLURM_SUBMIT_DIR}			# specifying working dir`<br/>

`# This below is the real part of the code!!`<br/>

`mkdir test`<br/>
`cd raw_reads/`<br/>
`for fastq in *.fastq.gz`<br/>
`do gunzip -c "$fastq" | paste - - - - | wc -l && echo $fastq `<br/>
`done > ../test/reads_raw.counts`

------------------ end code --------------------<br/>

So, what is this??? What are all those instructions? 

test.sb represents a "job." A file containing the code that
will perform the analysis and all the instructions
for the HPCC cluster about how much time we need, how much computational
power, how much RAM etc. to run the code and get the results

We will talk about it in class on Tuesday! So do 
some research an be ready to answer my questions.
Due to to the recent (unfortunately stil ongoing) migration of the
HPCC nodes to a new Operative system this below is a very useful link

https://wiki.hpcc.msu.edu/display/ITH/2018+Environment+Update+and+Migration

The last part of `test.sb` is the code itself, the bioinformatics script. 
Let's run it and see what we get.

`[benucci@dev-intel18 homework]$ sbatch test.sb`<br/>
`Submitted batch job 420139`<br/>

`[benucci@dev-intel18 homework]$ squeue -l -u benucci`<br/>
`Wed Oct 17 21:28:17 2018`<br/>
`             JOBID PARTITION     NAME     USER    STATE       TIME TIME_LIMI  NODES NODELIST(REASON)`<br/>
 `           420139 general-l prefilte  benucci  PENDING       0:00     10:00      1 (None)`<br/>
`[benucci@dev-intel18 homework]$`

When is done, navigate inside your folder and see what the code did,
we will talk about it on the next Tuesday 

If you need to contact me you can reach me by email, please see on
the top of this README.md file

## HAPPY CODING TO EVRYONE!!! ##
