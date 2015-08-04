CollectInsertSizeMetrics
========================

Command:

```bash
#!/bin/bash

BAM_INPUT=file.bam

java -Xmx4g -jar /usr/local/bioinfsoftware/picard-tools/current/jars/CollectInsertSizeMetrics.jar \
INPUT=${BAM_INPUT} \
HISTOGRAM_FILE=hist_plot.pdf \
OUTPUT=picard_insertSizeMetrics_output.txt
```

Results:


