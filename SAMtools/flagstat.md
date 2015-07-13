samtools flagstat 
=================
The `samtools flagstat` tool provides counts for each of 13 read categories
based primarily on bit flags in the FLAG field (**note that this refers to the
SAMtools released version 1.2 - February 2015**). Each category in the output
is broken down into QC pass and QC fail, which is presented as
"#PASS + #FAIL" followed by a description of the category.

The first row of output gives the total number of reads that are QC pass and
fail (according to flag bit 0x200). For example:

  122 + 28 in total (QC-passed reads + QC-failed reads)

Which would indicate that there are a total of 150 reads in the input file,
122 of which are marked as QC pass and 28 of which are marked as "not passing
quality controls"

Following this, additional categories are given for reads which are:

| Description | Flag |
|-------------|------|
|secondary | 0x100 bit set |
|supplementary | 0x800 bit set |
|duplicates | 0x400 bit set |
|mapped | 0x4 bit not set |
|paired in sequencing | 0x1 bit set |
|read1 | both 0x1 and 0x40 bits set |
|read2 | both 0x1 and 0x80 bits set |
|properly paired | both 0x1 and 0x2 bits set and 0x4 bit not set |
|with itself and mate mapped | 0x1 bit set and neither 0x4 nor 0x8 bits set |
|singletons | both 0x1 and 0x8 bits set and bit 0x4 not set |
|with mate mapped to a different chr | 0x1 bit set and neither 0x4 nor 0x8 bits set and MRNM not equal to RNAME |
|with mate mapped to a different chr (mapQ>=5) | 0x1 bit set and neither 0x4 nor 0x8 bits set and MRNM not equal to RNAME and MAPQ >= 5  |

The two last rows additionally filter on the reference
name (RNAME), mate reference name (MRNM), and mapping quality (MAPQ) fields.

Example output (from a sorted BAM file aligned with BWA-MEM, no duplicates flagged yet):

```
  1 480861162 + 0 in total (QC-passed reads + QC-failed reads)
  2 0 + 0 secondary
  3 3055712 + 0 supplementary
  4 0 + 0 duplicates
  5 475908985 + 0 mapped (98.97%:-nan%)
  6 477805450 + 0 paired in sequencing
  7 238902725 + 0 read1
  8 238902725 + 0 read2
  9 461777552 + 0 properly paired (96.65%:-nan%)
 10 472089012 + 0 with itself and mate mapped
 11 764261 + 0 singletons (0.16%:-nan%)
 12 5697922 + 0 with mate mapped to a different chr
 13 2424881 + 0 with mate mapped to a different chr (mapQ>=5)
```


References:

* SAMtools dev version: <https://github.com/samtools/samtools/blob/develop/samtools.1>
* Biostars1: <https://www.biostars.org/p/12475/>
