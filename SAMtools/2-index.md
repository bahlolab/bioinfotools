samtools index
==============

Index a coordinate-sorted BAM file for fast random access.

- If an output file is given, the index file will be written to
`out.index`.
- Otherwise, the index for a BAM file `sampleX.bam`  will be output to
the file `sampleX.bam.bai`.

Example BASH pipeline:

```bash
#!/bin/bash

BAM_DIR=../Data/
THIS_DIR=$(pwd -P)

cd $BAM_DIR

for bamFile in *.bam
do
        samtools index $bamFile &
done
```
