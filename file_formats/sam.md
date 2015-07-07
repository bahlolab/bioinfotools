The SAM Format Specification
============================
SAM stands for Sequence Alignment/Map format. It is a tab-delimited format consisting of a (optional) header section and an alignment section.

# The header section
The header lines (if existing) must be prior to the alignments. Each header line starts with a "@", followed by a two-letter record type code. Each line is tab-delimited and except the @CO lines, each data field follows a format "TAG:VALUE" where TAG is a two-letter string that defines the content and the format of VALUE. 

* @HD --> The header line. The first line if present.
	* VN*: Format version. (e.g. VN:1.4)
	* SO : Sorting order of alignments [unknown, unsorted, queryname and coordinate]. (e.g. SO:coordinate)

* @SQ --> Reference sequence dictionary. The order of @SQ lines defines the alignment sorting order.
	* SN*: Reference sequence name. Each @SQ line must have a unique SN tag. The value of this field is used in the alignment records in RNAME and PNEXT fields. (e.g. SN:chr1) 
	* LN*: Reference sequence length.(e.g. LN:249,250,621 for chr1)
	* AS : Genome assembly identifier. (e.g. AS:hg19substplus_gatk.ndx)

* @RG --> Read group. Unordered multiple @RG lines are allowed.
	* ID*: Read group identifier. Each @RG line must have a unique ID. The value of ID is used in the RG tags of alignment records. (e.g. ID:A803Y.1.N)
	* CN : Sequencing centre name where the read was produced (e.g. CN:AGRF).
	* DS : Description. (e.g. DS:cfDNA_urine_2014Mar11)
	* DT : Date the run was produced.
	* FO : Flow order. 
	* LB : Library. (e.g. LB:cfDNA_urine)
	* PG : Programs used for processing the read group.
	* PI : Predicted median insert size.
	* PL : Platform/technology used to produce the reads. (e.g. PL:ILLUMINA)
	* PU : Platform unit.
	* SM : Sample. (e.g. SM:SEN1-8)

* @PG --> Program.
	* ID*: Program record identifier. Each @PG line must have a unique ID. The value of ID is used in the alignment PG tag and PP tags of other @PG lines. PG IDs may be modified when merging SMA files in order to handle collisions. (e.g. ID:MarkDuplicates, ID:novoalign)
	* PN : Program name. (e.g. PN:MarkDuplicates, PN:novoalign)
	* CL : Command line. (e.g. CL:novoalign -c 2 -d hg19substplus_gatk.ndx -o FULLNW -k -K ...)
	* PP : Previous @PG-ID. Must match another @PG header's ID tag. (e.g. in a file with novoalign first and MarkDuplicates second you'd have PP:novoalign in the MarkDuplicates chunk)
	* DS : Description.
	* VN : Program version.

* @CO --> One-line text comment.


# The alignment section
Each alignment line has eleven mandatory fields for essential alignment information such as mapping position, and a number of optional fields for flexible or aligner specific information. For example check out the next three lines of reads.

M01158:9:000000000-A803Y:1:2105:10776:19681→    163→    chrM→   1→      70→     3I72M→  =→      189→    263→    ATGGATCACAGGTCTATCACCCTATTAACTACTCACGGGAGCTCTCCATGCATTTGGTAT    TTTCGTCTGGGGGGT→    ?;>=A>7-@B>/*@.C=;&@CC@C>@CCC&C&*&'.CA.A='7@?@7,8)D)%;&(DA?''?79A/=';7:>>7'→    LB:Z:cfDNA_urine→       MD:Z:26C36Y8→   PG:Z:MarkDuplicates→    RG:Z:A80    3Y.1.N→ AM:i:0→ NM:i:5→ SM:i:0→ PQ:i:122→       UQ:i:92→AS:i:92→PU:Z:PU
 99 M01158:9:000000000-A803Y:1:1104:14136:3297→     145→    chrM→   2→      20→     75M→    =→      16247→  16318→  ATCACAGGTCTATCACCCTATTAACCACTCACGGGAGCTCTCCATGCATTTGGTATTTTC    GTCTGGGGGGCATGC→    ADCB6BDDCCDADDB>EDDAAD@@AB?D,D@<C?(6A@:<>CC@CBC?C5CCBC?>,CCBBCAAAAAAAA??@8;→    LB:Z:cfDNA_urine→       MD:Z:62Y7T0R3→  PG:Z:MarkDuplicates→    RG:Z:A80    3Y.1.N→ NM:i:3→ UQ:i:37→AS:i:37→PU:Z:PU
100 M01158:9:000000000-A803Y:1:2111:25965:10335→    81→     chrM→   5→      20→     75M→    =→      16426→  16496→  ACAGGTCTATCACCCTATTAACCACTCACGGGAGCTCTCCATGCATTTGGTATTTTCGTC    TGGGGGGTATGCACG→    @CCDDEDEEEDDDDEEEEEDDEEDEEEDEDDDDDDEDEEDDEDDDEEEDCEDEEEECCECECCCCCCECEBBBA?→    LB:Z:cfDNA_urine→       MD:Z:59Y8R6→    PG:Z:MarkDuplicates→    RG:Z:A80    3Y.1.N→ NM:i:2→ UQ:i:6→ AS:i:6→ PU:Z:PU

## Mandatory fields
Each alignment line typically represents the linear alignment of a segment. Each line has 11 mandatory fields. These fields always appear in the same order and must be present, but their values can be '0' or '*' (depending on the field) if the corresponding information is unavailable.

1.  QNAME --> Query template NAME. (M01158:9:000000000-A803Y:1:2105:10776:19681→)
2.  FLAG  --> bitwise FLAG. (163→)
3.  RNAME --> Reference sequence NAME. (chrM→)
4.  POS   --> 1-based leftmost mapping POSition. (1→)
5.  MAPQ  --> MAPping Quality. (70→)
6.  CIGAR --> CIGAR string. (3I72M→)
7.  RNEXT --> Ref. name of the mate/NEXT read. (=→)
8.  PNEXT --> Position of the mate/NEXT read. (189→)
9.  TLEN  --> observed Template LENgth. (263→)
10. SEQ   --> segment SEQuence. (ATGGATCACAGGTCTATCACCCTATTAACTACTCACGGGAGCTCTCCATGCATTTGGTAT→)
11. QUAL  --> ASCII of Phred-scaled base QUALity+33. (?;>=A>7-@B>/*@.C=;&@CC@C>@CCC&C&*&'.CA.A='7@?@7,8)D)%;&(DA?''?79A/=';7:>>7'→)

## Optional fields
All optional fields follow the TAG:TYPE:VALUE format where TAG is a two-character string. Each TAG can only appear once in one alignment line. TYPE is a single case-sensitive letter defining the format of VALUE.

Type - Description:
1. A - Printable character.
2. i - Single 32-bit integer.
3. f - Single-precision floating number.
4. Z - Printable string, including space.
5. H - Byte array in the Hex format.
6. B - Integer or numeric array.

Examples: LB:Z:cfDNA_urine, AM:i:0.



