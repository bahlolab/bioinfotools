Picard SamToFastq
=================
Extracts read sequences and qualities from the input SAM/BAM file and writes
them into the output file in Sanger fastq format.

Example bash script
-------------------

```bash
#!/bin/bash

BATCH=1
BAM_PATH=BAM_dir/batch${BATCH}
FASTQ_PATH=Data/FASTQ_dir
PICARD_DIR=bioinfsoftware/picard-tools/current/jars

for bam in ${BAM_PATH}/*rmdup.bam
do
        (
        echo "The file is $bam"
        # extract only the basename without the extension
        SAMP=$(basename "$bam" .picard.sorted.RG.realigned.rmdup.bam)
        echo "This is sample $SAMP"
        SAMP_DIR=${FASTQ_PATH}/${SAMP}
        mkdir -p $SAMP_DIR

        IN_BAM=$bam

        start=$(date +%s.%N)

        java -Xmx4g -Djava.io.tmpdir=`pwd`/tmp -jar $PICARD_DIR/RevertSam.jar \
        INPUT=$IN_BAM \
        OUTPUT=/dev/stdout \
        SORT_ORDER=queryname \
        COMPRESSION_LEVEL=0 \
        VALIDATION_STRINGENCY=SILENT | java -Xmx4g -Djava.io.tmpdir=`pwd`/tmp \
        -jar $PICARD_DIR/SamToFastq.jar \
        INPUT=/dev/stdin \
        OUTPUT_PER_RG=true \
        OUTPUT_DIR=$SAMP_DIR \
        VALIDATION_STRINGENCY=SILENT

        end=$(date +%s.%N)
        runtime=$(python -c "print(${end} - ${start})")
        echo "Runtime for ${IN_BAM} was ${runtime}"
        ) &

done
```

Description:
<http://broadinstitute.github.io/picard/command-line-overview.html#SamToFastq>
