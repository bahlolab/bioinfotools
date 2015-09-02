
Example BASH script:

```bash
#!/bin/bash

BAM_DIR=../../Data/
THIS_DIR=$(pwd -P)

cd $BAM_DIR

for bamFile in *.bam
do
        samtools idxstats ${bamFile} >> ${THIS_DIR}/${bamFile}_idxstats.txt &
done
```
