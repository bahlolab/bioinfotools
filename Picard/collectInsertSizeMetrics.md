CollectInsertSizeMetrics
========================

Usage info:
http://broadinstitute.github.io/picard/command-line-overview.html#CollectInsertSizeMetrics

Command Example:

```bash
#!/bin/bash

BAM_INPUT=file.bam

java -Xmx4g -jar /usr/local/bioinfsoftware/picard-tools/current/jars/CollectInsertSizeMetrics.jar \
INPUT=${BAM_INPUT} \
HISTOGRAM_FILE=hist_plot.pdf \
OUTPUT=picard_insertSizeMetrics_output.txt
```

Results:

* nohup file (STDOUT):

```
[Tue Aug 04 12:46:54 EST 2015] picard.analysis.CollectInsertSizeMetrics HISTOGRAM_FILE=hist_file.pdf INPUT=file.bam OUTPUT=picard_insertSizeMetrics_output.txt
...DEVIATIONS=10.0 MINIMUM_PCT=0.05 METRIC_ACCUMULATION_LEVEL=[ALL_READS] ASSUME_SORTED=true STOP_AFTER=0 VERBOSITY=INFO QUIET=false VALIDATION_STRINGENCY=STRICT
...COMPRESSION_LEVEL=5 MAX_RECORDS_IN_RAM=500000 CREATE_INDEX=false CREATE_MD5_FILE=false
[Tue Aug 04 12:46:54 EST 2015] Executing as diakumis@unix301.wehi.edu.au on Linux 2.6.32-358.el6.x86_64 amd64; Java HotSpot(TM) 64-Bit Server VM 1.7.0_03-b04; Picard version: 1.117(107...) JdkDeflater
INFO   2015-08-04 12:47:02    SinglePassSamProgram   Processed     1,000,000 records.  Elapsed time: 00:00:07s.  Time for last 1,000,000:    7s.  Last read position: chrM:15,157
INFO   2015-08-04 12:47:10    SinglePassSamProgram   Processed     2,000,000 records.  Elapsed time: 00:00:15s.  Time for last 1,000,000:    7s.  Last read position: chr1:1,262,633
INFO   2015-08-04 12:47:17    SinglePassSamProgram   Processed     3,000,000 records.  Elapsed time: 00:00:22s.  Time for last 1,000,000:    7s.  Last read position: chr1:2,616,195
...
...
...
INFO   2015-08-04 18:14:33    SinglePassSamProgram   Processed 2,504,000,000 records.  Elapsed time: 05:27:38s.  Time for last 1,000,000:    7s.  Last read position: chrX:153,433,357
INFO   2015-08-04 18:14:40    SinglePassSamProgram   Processed 2,505,000,000 records.  Elapsed time: 05:27:46s.  Time for last 1,000,000:    7s.  Last read position: chrX:154,666,522
INFO   2015-08-04 18:14:49    SinglePassSamProgram   Processed 2,506,000,000 records.  Elapsed time: 05:27:54s.  Time for last 1,000,000:    8s.  Last read position: chrY:1,974,022
INFO   2015-08-04 18:14:57    SinglePassSamProgram   Processed 2,507,000,000 records.  Elapsed time: 05:28:02s.  Time for last 1,000,000:    8s.  Last read position: chrY:13,141,012
INFO   2015-08-04 18:15:06    SinglePassSamProgram   Processed 2,508,000,000 records.  Elapsed time: 05:28:11s.  Time for last 1,000,000:    9s.  Last read position: chrY:13,454,221
...
...
...
INFO   2015-08-04 18:20:57    SinglePassSamProgram   Processed 2,553,000,000 records.  Elapsed time: 05:34:02s.  Time for last 1,000,000:    8s.  Last read position: chrUn_gl000234:8,022
INFO   2015-08-04 18:21:05    SinglePassSamProgram   Processed 2,554,000,000 records.  Elapsed time: 05:34:10s.  Time for last 1,000,000:    7s.  Last read position: chrUn_gl000246:11,625
INFO   2015-08-04 18:22:34    RExecutor       Executing R script via command: Rscript /tmp/diakumis/script7190408885514757563.R picard_insertSizeMetrics_output.txt hist_file.txt file.bam
INFO    2015-08-04 18:22:36     ProcessExecutor null device 
INFO    2015-08-04 18:22:36     ProcessExecutor           1 
[Tue Aug 04 18:22:36 EST 2015] picard.analysis.CollectInsertSizeMetrics done. Elapsed time: 335.70 minutes.
Runtime.totalMemory()=1733230592
```

* main program output (transposed using bahlolab/utils/transpose):

```
MEDIAN_INSERT_SIZE        380
MEDIAN_ABSOLUTE_DEVIATION 57
MIN_INSERT_SIZE           2
MAX_INSERT_SIZE           244358811
MEAN_INSERT_SIZE          385.327046
STANDARD_DEVIATION        90.989072
READ_PAIRS                708037518
PAIR_ORIENTATION          FR
WIDTH_OF_10_PERCENT       23
WIDTH_OF_20_PERCENT       45
WIDTH_OF_30_PERCENT       67
WIDTH_OF_40_PERCENT       91
WIDTH_OF_50_PERCENT       115
WIDTH_OF_60_PERCENT       145
WIDTH_OF_70_PERCENT       181
WIDTH_OF_80_PERCENT       227
WIDTH_OF_90_PERCENT       301
WIDTH_OF_99_PERCENT       547
SAMPLE
LIBRARY
READ_GROUP
```

* Histogram output (plotted using additional output in the main program output
file and modified for this example):

![Figure insert_size_hist](../img/picard/insert_size_hist.png?raw=true)

