FastQC Documentation
====================

## Introduction
FastQC is a Java program developed by the Babraham Institute (near Cambridge
UK). It calculates various quality control metrics for MPS data and
outputs helpful plots which can be used to infer if the data is of expected
quality.  Modules include per base sequence quality, per sequence quality
scores, per sequence GC content, sequence duplication levels and others.

## Usage
We use it as part of our MPS pipeline but you can run it on the command line or
a bash script as:

```bash
fastqc foo
```

## Output
### fastqc\_data.txt
The `fastqc_data.txt` file contains the actual data/results which
FastQC uses for the plots. Each module has its own section
in this file, so you can easily look more closely into statistics of interest.

### Modules
#### Sequence Duplication Plot
The "Sequence Duplication Plot" is a bit tricky to interpret. 
This basically looks in your file for the first 200,000 different reads, and
tracks each one of them up to the end of the file, noting how many times each
one occurred.

Let's look at a sample output from FastQC v0.10.0 (from sample SEN1-10 WES
FASTQ):

```
>>Sequence Duplication Levels	warn
#Total Duplicate Percentage	40.61964181293796
#Duplication Level	Relative count
1	100.0
2	34.464139669186984
3	13.265067681471466
4	6.100512409660674
5	3.192128586450353
6	1.8785572413332665
7	1.2810241516866123
8	0.8403852252432694
9	0.6175621317577153
10++	5.269307162051642
>>END_MODULE
```

And here is the plot:

![Figure fastqc-old](img/fastqc/dup_levels_old.png?raw=true)

As you can see above, the y-axis scale is a bit problematic. As David Andrews
suggests in his 2011 blog post, this happens intentionally in order to save
computational memory. So the number of sequences occurring exactly once is set
to 100%, and all other values are relative to that number. This has several
issues, which are mentioned in his post.

The plot has changed in the latest v0.11.2 (from sample DYST2-3 WGS
recalibrated BAM):

```
>>Sequence Duplication Levels	pass
#Total Deduplicated Percentage	70.47067783055486
#Duplication Level	Percentage of deduplicated	Percentage of total
1	91.85755092943762	64.73263877852183
2	4.4519227092629245	6.274600219419971
3	1.1588137884920218	2.4498717946327804
4	0.4789029858848246	1.3499447212152096
5	0.2518703630262994	0.8874737603945622
6	0.15076918685790822	0.6374884076303027
7	0.11909634345473874	0.5874960035277205
8	0.09977599783506882	0.562502575892582
9	0.07292353458308728	0.46250738206830627
>10	1.3149233747757365	20.216737060219785
>50	0.04291771368166456	1.7760613060545531
>100	5.065942545384075E-4	0.050082797065918644
>500	2.6478453574855642E-5	0.01259519335644345
>1k	0.0	0.0
>5k	0.0	0.0
>10k+	0.0	0.0
>>END_MODULE
```

And here is the plot:

![Figure fastqc-new](img/fastqc/dup_levels_new.png?raw=true)

The y-axis represents a percentage of the total library, so
all values are much easier to understand. The x-axis categories have been
increased in order to get a clearer understanding of the duplication level. 
Finally, the plot has two lines instead of one, which refer to the raw and
deduplicated libraries. See the 2013 blog post for a nice example.

**References**

* <http://www.bioinformatics.babraham.ac.uk/projects/fastqc/>
* <http://proteo.me.uk/2013/09/a-new-way-to-look-at-duplication-in-fastqc-v0-11/>
* <http://proteo.me.uk/2011/05/interpreting-the-duplicate-sequence-plot-in-fastqc/>
