samtools sort
============
Sort alignments by leftmost coordinates (default), or by read name when -n is
used. An  appropriate  @HD-SO  sort  order header tag will be added or an
existing one updated if necessary.

## Usage

* Old style (before samtools v1.0): 
`samtools sort [options...] <in.bam> <out.prefix>`
    * Options:
      * `f`      : Use <out.prefix> as full final filename rather than prefix
      * `o`      : Write final output to stdout rather than <out.prefix>.bam
      * `l,m,n,@`: Similar to corresponding options below

* New style:
`samtools sort [-l level] [-m maxMem] [-o out.bam] [-O format] [-n] -T out.prefix [-@ threads] [in.bam]`
    * Options:
      * `l`: compression level
      * `m`: max memorey required per thread (default: 768 MB)
      * `o`: write sorted output to file instead of STDOUT
      * `O`: write to SAM, BAM or CRAM format. Use this when you want output to
      STDOUT
      * `n`: sort by read names (i.e., the QNAME field) rather than by
      chromosomal coordinates
      * `T`: write tmp files to `out.prefix.bam`
      * `@`: number of sorting and compression threads (default: 1)

## Example

First let's view the header and the first few reads in an example BAM file:

```bash
$ samtools view -h ../file_formats/example_files/exampleBAM.bam | head -n 8
@HD	VN:1.0	GO:none	SO:coordinate
@SQ	SN:chr1	LN:100000	AS:HG18	UR:/seq/references/Homo_sapiens_assembly18/v0/Homo_sapiens_assembly18.fasta	M5:9ebc6df9496613f373e73396d5b3b6b6	SP:Homo sapiens
@RG	ID:exampleBAM.bam	PL:illumina	PU:exampleBAM.bam	LB:exampleBAM.bam	SM:exampleBAM.bam
@PG	ID:0	VN:0.7.1-9	CL:picard/current/maq map [....]
30PPJAAXX090125:1:42:512:1817#0	99	chr1	200	0	76M	=	255	-130	ACCCTAACCCTAACCCTAACCCTAACCATAACCCTAAGACTAACCCTAAACCTAACCCTCATAATCGAAATACAAC	BBBBC@C?AABCBB<63>=B@>+B9-9+)2B8,+@327B5A>90((>-+''3?(/'''A)(''19('7.,**%)3:	PG:Z:0	RG:Z:exampleBAM.bam	SM:Z:exampleBAM.bam
30PPJAAXX090125:1:42:512:1817#0	147	chr1	255	2	76M	=	200	-130	CAACCCCAGCCCAAACCCGAACCCAAACCCGAACCCGAACCCTAACCCAACCCCCAACCCCAACCCTAACCCTAAC	2+&:A=4?'8@'%2'=>B3A3<A='A=A9>&>;A?A,@&>A?1A:AAB5=&9>7&:,@A<*70@B=9:0>@@2;=3	PG:Z:0	RG:Z:exampleBAM.bam	SM:Z:exampleBAM.bam
30PPJAAXX090125:1:60:1109:517#0	73	chr1	257	0	76M	=	257	0	ACCCTAACCCTAAACATAAACCTAACCCTAACCTGAACCTTATCCAGAACCCCAACTCGAACAAAAGTCGTAACCT	===<4:67(=>@>B?>BB=;::87=?9@B?=((*>1@6B:)8'85%%=,+(-7923%7<,0)4/'-1(.('02-9'	PG:Z:0	RG:Z:exampleBAM.bam	SM:Z:exampleBAM.bam
30PPJAAXX090125:1:67:744:1312#0	163	chr1	10399	0	76M	=	10479	-155	GGAAATTTACAAGGAACAAATGTGAAGCACAACATTTAGGTTTTAAAAATCAAGCGAATAAATACAGAAGGTGGAG	):CCBAABBBCCBC?=-=CC=@A?ACCB==CCC:ABBBBC=B@BA=ABCCBCCACC-=CCBCCCBCB2>><22BAB	PG:Z:0	RG:Z:exampleBAM.bam	SM:Z:exampleBAM.bam
```

And now let's sort this by query name:

```bash
samtools view -h ../file_formats/example_files/exampleBAM.bam | samtools sort -n -O sam -T aln.qsort | head -n 8
@HD	VN:1.0	GO:none	SO:queryname
@SQ	SN:chr1	LN:100000	AS:HG18	UR:/seq/references/Homo_sapiens_assembly18/v0/Homo_sapiens_assembly18.fasta	M5:9ebc6df9496613f373e73396d5b3b6b6	SP:Homo sapiens
@RG	ID:exampleBAM.bam	PL:illumina	PU:exampleBAM.bam	LB:exampleBAM.bam	SM:exampleBAM.bam
@PG	ID:0	VN:0.7.1-9	CL:picard/current/maq map [....]
30PPJAAXX090125:1:13:176:419#0	83	chr1	30014	0	76M	=	29967	-122	GATGAGAACTCAGTGCTGGCTGACACCCTGATGGCACCTTACAGAGGACCAGTTAGGCTGTGCCAACTCCTGACCT	6:<AA=7+:)??8?5?=5=A@=?A69A4A@BB?(@4@@B?AAA?B87;?AB:BBC6?>?7B=?>B5;AAAB<<BAB	PG:Z:0	RG:Z:exampleBAM.bam	SM:Z:exampleBAM.bam
30PPJAAXX090125:1:13:176:419#0	163	chr1	29967	0	76M	=	30014	-122	CTGCCATGTGAGCTTGGAAGCAGAGCCATCCACACAGCTGAGCCCTAGATGAGAACGCAGTGCTGGCTGACACCCT	B@27@BCCCBCACB=CBBBB9CB@8/BBC@)7AB;ABBC>>>>BACB=?>;BA>@:?>9B9>3?BA=B<B=B'6-@	PG:Z:0	RG:Z:exampleBAM.bam	SM:Z:exampleBAM.bam
30PPJAAXX090125:1:14:920:883#0	83	chr1	57554	0	76M	=	57504	-125	AATTGAAATGGCTCTCAACTCATGCCCAGAAGTCAGTGTTCAGTCTCTCACCTGGCAGATAGCAACTTAGAAAGAT	A=5:B?A?;A@@<@>@>@B<B@@B?:A?B@?B@A@BABA<B@BA:<>=1:B?;BBBBB:@BBA7?BBB>2BCCBCA	PG:Z:0	RG:Z:exampleBAM.bam	SM:Z:exampleBAM.bam
30PPJAAXX090125:1:14:920:883#0	163	chr1	57504	0	76M	=	57554	-125	TTCACTGCAAAACTTCTTGAAACAGTACTTATTTTCTCTCCTCCATACACAATTGAAATGGCTCTCAACTCATGCC	;@CCCCCBCACC?CACCCACCCCCCCCCBCCCCCCCCCBCCCCB5BCCBBCACCC@BCCCACBCCBBCC?BCCA@<	PG:Z:0	RG:Z:exampleBAM.bam	SM:Z:exampleBAM.bam
```

We can notice that the `@HD SO` tag has changed from `coordinate` to `queryname`,
while the reads are now sorted by their first field i.e. the read name.
