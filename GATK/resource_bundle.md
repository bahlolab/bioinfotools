GATK Resource Bundle
====================
## Introduction
The GATK resource bundle is a collection of standard files for working with
human resequencing data with the GATK.

## Bundle Access
The bundles are available on the GATK public FTP server.

* If you're using an FTP client (e.g. FileZilla, Cyberduck etc.), you can
download from `ftp.broadinstitute.org`, using the username
`gsapubftp-anonymous` and leaving the password blank.
* If you're using a web browser (e.g. Chrome, FireFox), you can download from 
<ftp://ftp.broadinstitute.org/bundle>.


## Bundle contents
The `bundle` directory contains a folder for each release (e.g. 2.8). Inside
each folder there are four other directories: b36, b37, hg18 and hg19.

```
bundle
|--2.8
  |--b36
  |--b37
  |--hg18
  |--hg19
  |--exampleFASTA
|--2.5
  |--b36
  |--b37
  |--hg18
  |--hg19
  |--exampleFASTA
```

These are the contents of b37 (hg19 is very similar, except that the
reference sequence is called `ucsc.hg19.fasta.gz` and the `dbsnp_138` version
is used):

```
Reference Sequence
|--human_g1k_v37.fasta.gz
   human_g1k_v37.fasta.fai.gz
   human_g1k_v37.dict.gz
|--human_g1k_v37_decoy.fasta.gz
   human_g1k_v37_decoy.fasta.fai.gz
   human_g1k_v37_decoy.dict.gz

dbSNP recent release
|--dbsnp_137.b37.vcf.gz
   dbsnp_137.b37.vcf.idx.gz

dbSNP with sites discovered in or before dbSNPBuildID 129, which excludes the
impact of the 1KG project and is useful for evaluation of dbSNP rate and Ti/Tv
values at novel sites.
|--dbsnp_137.b37.excluding_sites_after_129.vcf.gz
   dbsnp_137.b37.excluding_sites_after_129.vcf.idx.gz

HapMap genotypes and sites
|--hapmap_3.3.b37.vcf.gz
   hapmap_3.3.b37.vcf.idx.gz

OMNI 2.5 genotypes for 1KG samples and sites
|--1000G_omni2.5.b37.vcf.gz
   1000G_omni2.5.b37.vcf.idx.gz

The current best set of known indels for local realignment (note that dbSNP
isn't used for this anymore)
|--1000G_phase1.indels.b37.vcf.gz
   1000G_phase1.indels.b37.vcf.idx.gz
|--Mills_and_1000G_gold_standard.indels.b37.vcf.gz
   Mills_and_1000G_gold_standard.indels.b37.vcf.idx.gz

Large-scale standard single sample BAM file for testing
|--NA12878.HiSeq.WGS.bwa.cleaned.raw.subset.b37.sites.vcf.gz
   NA12878.HiSeq.WGS.bwa.cleaned.raw.subset.b37.sites.vcf.idx.gz
   NA12878.HiSeq.WGS.bwa.cleaned.raw.subset.b37.vcf.gz
   NA12878.HiSeq.WGS.bwa.cleaned.raw.subset.b37.vcf.idx.gz
   NA12878.knowledgebase.snapshot.20131119.b37.vcf.gz
   NA12878.knowledgebase.snapshot.20131119.b37.vcf.idx.gz
|--CEUTrio.HiSeq.WGS.b37.NA12878.bam
   CEUTrio.HiSeq.WGS.b37.NA12878.bam.bai.gz
   CEUTrio.HiSeq.WGS.b37.NA12878.vcf.gz
   CEUTrio.HiSeq.WGS.b37.NA12878.vcf.idx.gz

(Not mentioned)
|--1000G_phase1.snps.high_confidence.b37.vcf.gz
   1000G_phase1.snps.high_confidence.b37.vcf.idx.gz
|--Broad.human.exome.b37.interval_list.gz
|--CEUTrio.HiSeq.WGS.b37.bestPractices.phased.b37.vcf.gz
   CEUTrio.HiSeq.WGS.b37.bestPractices.phased.b37.vcf.idx.gz

```

## Differences between b37 and hg19

The Genome Reference Consortium (GRC) periodically releases a version
of the human genome e.g. in February 2009 they released "build 37", which is
known as GRCh37.

| UCSC Version | Release Date | Release Name |
|--------------|--------------|--------------|
| hg18         | Mar 2006     | NCBI b36     |
| hg19         | Feb 2009     | GRCh37       |
| hg38         | Dec 2013     | GRCh38       |

Each version includes the following sequences:

* 24 "relatively complete" sequences for chromosomes 1-22, X and Y;
* A complete mitochondrial sequence;
* Several "unlocalised sequences" - known chromosome, unknown coordinates;
* Several "unplaced sequences" - known from human, unknown chromosome;
* Several "alternate loci" - sequences with alternate representations of
specific human regions;

The GRC didn't provide a set of naming rules for these sequences, so different
teams adopted different rules:

* The **b37** conventions were used by the 1KG Project. GATK and IGV use this
name. The ENSEMBL genome browser, the NCBI dbSNP database (in VCF files) and
the Sanger COSMIC database (in VCF files) are among those preferring these
conventions. These are also the preferred standards for new projects.
* The **hg19** conventions were used by the UCSC genome browser. Despite the
old mitochondrial sequence, the nonstandard naming and the inclusion of
alternate loci (which are undesirable for read mapping), hg19 has gained
popularity due to its exposure via the UCSC genome browser, and is often the
convention used by vendors when reporting exome enrichment kit coordinates.

In summary the differences are:

1. Naming conventions:
  - b37: 1-22, X, Y, MT;
  - hg19: chr1-chr22, chrX, chrY, chrM;
1. Mitochondrial sequence:
  - b37 has an updated one;
  - hg19 has an older one from build 36;
1. Unlocalised and unplaced sequences:
  - b37: named after their accession numbers e.g. "GL000191.1";
  - hg19: given custom names e.g. "chr1\_gl000191\_random", "chrUn\_gl000221";
1. Alternate loci:
  - b37: not included;
  - hg19: included;


## Which version should I use?
It's suggested to use the extended "decoy" version of b37 which includes
human herpesvirus sequence and a decoy sequence derived from HuRef (Craig
Venter genome), humen BAC and Fosmid clones, and NA12878 (named "hs37d5"). It
also has the pseudo-autosomal regions (PAR) of chromosome Y masked out
(replaced with "N") so that the respective regions in chromosome X may be
treated as diploid. In summary:
  - used by the 1KG in Phase II;
  - provides better results due to the PAR masking and the addition of the
  decoy sequences;
  - supported by GATK and IGV;
  - compatible with all the annotations (dbSNP etc.) that are reported using
  the "b37" conventions. 

**References**

* GATK download: <https://www.broadinstitute.org/gatk/download/>
* Bundle location: <https://www.broadinstitute.org/gatk/guide/article?id=1215>
* Bundle contents: <http://gatkforums.broadinstitute.org/discussion/1213/whats-in-the-resource-bundle-and-how-can-i-get-it>
* b37 vs. hg19:
  - <https://answers.dnanexus.com/p/183/>
  - <https://wiki.dnanexus.com/Scientific-Notes/human-genome>
  - <http://gatkforums.broadinstitute.org/discussion/1810/whats-the-difference-between-b37-and-hg19-resources>
  - <http://genome.ucsc.edu/FAQ/FAQreleases.html>
  - <https://www.biostars.org/p/6918/>
