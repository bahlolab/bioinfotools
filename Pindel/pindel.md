Pindel
======

Introduction
------------
Pindel is a program written in C++ that is used to detect breakpoints of large
deletions, medium sized insertions, inversions, tandem duplications and other
structural variants at single-based resolution from NGS data. It uses a pattern
growth approach to identify the breakpoints of these variants from paired-end
short reads.

Resources
---------
* Webpage: http://gmt.genome.wustl.edu/packages/pindel/index.html
* GitHub: https://github.com/genome/pindel

Installation
------------

```bash
# get the code
git clone git://github.com/genome/pindel.git

# compile source code
cd pindel
./INSTALL /path/to/samtools_folder/

# test it out
cd demo
../pindel -f simulated_reference.fa -i simulated_config.txt -o output
```

Running
-------

```bash
#!/bin/bash

reference=${db}/hg19/standard_gatk/hg19.fa
family=foo
email=me@foo.edu.au

BAM_CONFIG_FILE=${family}_bam_config.txt
THREADS=6

mkdir -p output

start_time=`date +%s`
echo "Pindel starting at ${start_time}"
pindel -f $reference -i $BAM_CONFIG_FILE -c ALL -o output/pindel_${family}_ -T $THREADS
end_time=`date +%s`
echo "Pindel finishing at `date`"
echo "Execution time was `expr $end_time - $start_time` s."
echo "Pindel has finished in directory" $(pwd) "on host:" $HOSTNAME | mail -s "${family} pindel analysis finished on $HOSTNAME" $email
```
