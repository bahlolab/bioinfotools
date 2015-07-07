samtools view
===============

With no options specified, `view` prints all the reads in the specified input
alignment file (SAM/BAM/CRAM format) to STDOUT in SAM format (without header).

You can see the available command-line options using `man samtools.1`:

| Option | Description |
|----|-----------------------------|
| -b | Output in BAM format        |
| -B | Collapse the backward CIGAR operation |
| -c | Count number of reads, don't print them |
| -C | Output in CRAM format (requires `-T`) |
| -f INT | Output reads with all bits set in INT present in FLAG field |
| -F INT | Do not output reads with any bits set in INT present in FLAG field |
| -h | Include header in output    |
| -H | Only header in output       |
| -l STR | Output reads in library STR [null] |
| -L FILE | Output reads overlapping the BED FILE [null] |
| -m INT | Output reads with number of CIGAR bases consuming query seq >= INT [0] |
| -o FILE | Output to FILE [STDOUT] |
| -q INT | Skip reads with MAPQ < INT [0] |
| -r STR | Output reads in read group STR [null] |
| -R FILE | Output reads in read groups listed in FILE [null] |
| -s FLOAT | Random sample with seed + percent reads |
| -S | Input is in SAM (not required any more since format autodetected now) |
| -t FILE | Tab-delimited FILE with reference name/length in columns 1-2 |
| -T FILE | A FASTA format reference FILE |
| -u | Output uncompressed BAM. Preferred with pipes |
| -U FILE | Write filtered (unselected) reads to FILE |
| -x STR | Read tag to exclude from output (repeatable) [null] |
| -1 | Enable fast BAM compression (implies `-b`) |
| -? | Help                        |
| -@ INT | Number of BAM compression threads in addition to main thread [0] |

## Examples

### View all reads

* From BAM to SAM (without header)

```bash
samtools view exampleBAM.bam
```

* From BAM to SAM (with header)

```bash
samtools view -h exampleBAM.bam
```

* View SAM header only

```bash
samtools view -H exampleBAM.bam
```

* From SAM to BAM

```bash
samtools view -Sb exampleSAM.sam > exampleBAM_2.bam
# samtools view -b exampleSAM.sam > exampleBAM_2.bam
```


### Filter

* Count total reads

```bash
samtools view -c exampleBAM.bam
```

* Count total mapped reads

```bash
samtools view -c -F0x4 exampleBAM.bam
```
