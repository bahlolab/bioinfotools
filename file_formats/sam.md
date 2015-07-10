The SAM Format Specification
============================
SAM stands for Sequence Alignment/Map format. It is a tab-delimited format
consisting of a header section, which is optional, and an alignment section.

# The header section
The header lines (if existing) must be prior to the alignments.
Each header line starts with a "@", followed by a two-letter record type code.
Each line is tab-delimited and (except the @CO (comment) lines) each data
field follows a format "TAG:VALUE" where TAG is a two-letter string that
defines the content and the format of VALUE.
The record types and tags used are (starred tags are required when record type
is used):

| Tag   | Description |
|-------|-------------|
| **@HD** | Header line (first line). Example: `@HD  VN:1.0  GO:none SO:coordinate `|
| VN* | Version of format |
| SO  | Sorting order [unknown (def), unsorted, queryname, coordinate] |
| GO  | Grouping of reads [none (def), query, reference] |
|||
| **@SQ** | Reference sequence dictionary, defining order of reads. Example: `@SQ SN:chr1 LN:249250621 AS:HG19 UR:hg19.fasta M5:9ebc6 SP:Homo sapiens` |
| SN* | Refseq name. Must be unique for each line |
| LN* | Refseq length |
| AS  | Genome assembly identifier |
| M5  | MD5 checksum of the read |
| SP  | Species |
| UR  | URI of the sequence |
|||
| **@RG** | Read group. Unordered multiple @RG lines are allowed. Example: `@RG ID:exBAM.bam CN:AGRF DS:example_1 DT:Aug2015 PL:illumina  PU:exBAM.bam LB:exBAM.bam SM:exBAM.bam` |
| ID* | Read group identifier. Must be unique for each RG line. Used in read RG tags |
| CN | Sequencing centre name where the read was produced                   |
| DS | Description. (e.g. DS:cfDNA_urine_2014Mar11)                         |
| DT | Date the run was produced                                            |
| FO | Flow order                                                           |
| LB | Library                                                              |
| PG | Programs used for processing the read group                          |
| PI | Predicted median insert size                                         |
| PL | Platform/technology used to produce the reads                        |
| PU | Platform unit                                                        |
| SM | Sample                                                               |
|||
| **@PG** | Program. Example: `@PG  ID:novoalign  PN:novoalign  VN:V3.02.00 CL:novoalign foo bar baz` |
| ID* | Program ID. Must be unique for each @PG line. Used in read PG tag and PP tags of other @PG lines. |
| PN  | Program name |
| CL  | Command line (long...) |
| PP  | Previous @PG-ID. Must match another @PG header's ID tag (e.g. in a file with novoalign first and MarkDuplicates second you'd have PP:novoalign in the MarkDuplicates chunk) |
| DS  | Description |
| VN  | Program version |
|||
| **@CO** | One-line text comment. Multiple @CO lines allowed |

# The alignment section
Each alignment line has eleven mandatory fields for essential alignment
information such as mapping position and quality, and a number of optional
fields for other information.

Here are three example read alignment lines (from exampleBAM.bam):

```
30PPJAAXX090125:1:42:512:1817#0	99	chr1	200	0	76M	=	255	-130	ACCCTAACCCTAACCCTAACCCTAACCATAACCCTAAGACTAACCCTAAACCTAACCCTCATAATCGAAATACAAC	BBBBC@C?AABCBB<63>=B@>+B9-9+)2B8,+@327B5A>90((>-+''3?(/'''A)(''19('7.,**%)3:	PG:Z:0	RG:Z:exampleBAM.bam	SM:Z:exampleBAM.bam
30PPJAAXX090125:1:42:512:1817#0	147	chr1	255	2	76M	=	200	-130	CAACCCCAGCCCAAACCCGAACCCAAACCCGAACCCGAACCCTAACCCAACCCCCAACCCCAACCCTAACCCTAAC	2+&:A=4?'8@'%2'=>B3A3<A='A=A9>&>;A?A,@&>A?1A:AAB5=&9>7&:,@A<*70@B=9:0>@@2;=3	PG:Z:0	RG:Z:exampleBAM.bam	SM:Z:exampleBAM.bam
30PPJAAXX090125:1:60:1109:517#0	73	chr1	257	0	76M	=	257	0	ACCCTAACCCTAAACATAAACCTAACCCTAACCTGAACCTTATCCAGAACCCCAACTCGAACAAAAGTCGTAACCT	===<4:67(=>@>B?>BB=;::87=?9@B?=((*>1@6B:)8'85%%=,+(-7923%7<,0)4/'-1(.('02-9'	PG:Z:0	RG:Z:exampleBAM.bam	SM:Z:exampleBAM.bam
```

## Mandatory fields
These fields always appear in the same order and must be present,
but their values can be '0' or '*' (depending on the field) if the
corresponding information is unavailable.

|Col |Field | Description               | Example                  |
|----|------|---------------------------|--------------------------|
| 1  |QNAME | Query (read) NAME | `30PPJAAXX090125:1:42:512:1817#0`|
| 2  |FLAG  | bitwise FLAG | `99` |
| 3  |RNAME | Reference sequence NAME | `chr1` |
| 4  |POS   | 1-based leftmost mapping POSition | `200` |
| 5  |MAPQ  | MAPping Quality | `0` |
| 6  |CIGAR | CIGAR string | `76M` |
| 7  |RNEXT | Ref name of the mate/NEXT read | `=` |
| 8  |PNEXT | Position of the mate/NEXT read | `255` |
| 9  |TLEN  | observed Template LENgth | `-130` |
| 10 |SEQ   | segment SEQuence | `ACCCTAACCCTAACCCTAACCCTAACCATAACCCTAAGACTAACCCTAAACCTAACCCTCATAATCGAAATACAAC` |
| 11 |QUAL  | ASCII of Phred-scaled base QUALity+33 | `BBBBC@C?AABCBB<63>=B@>+B9-9+)2B8,+@327B5A>90((>-+''3?(/'''A)(''19('7.,**%)3:` |

## Optional fields
All optional fields follow the TAG:TYPE:VALUE format where TAG is a two-character string. Each TAG can only appear once in one alignment line. TYPE is a single case-sensitive letter defining the format of VALUE.

| Type | Description |
|------|-------------|
| A | Printable character               |
| i | Single 32-bit integer             |
| f | Single-precision floating number  |
| Z | Printable string, including space |
| H | Byte array in the Hex format      |
| B | Integer or numeric array          |

Example: `PG:Z:0	RG:Z:exampleBAM.bam	SM:Z:exampleBAM.bam`

## Flags
The unmapped reads (Flag 4) are given the chromosome and position of their
mapped mate.


Sources:

* <https://www.biostars.org/p/14569/>
* <https://www.biostars.org/p/18949/>
* <https://www.biostars.org/p/12475/>


