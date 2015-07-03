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

Let's look first at b37:

```
Reference Sequence
|--human_g1k_v37.fasta.gz
   human_g1k_v37.fasta.fai.gz
   human_g1k_v37.dict.gz

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

|--1000G_phase1.snps.high_confidence.b37.vcf.gz
   1000G_phase1.snps.high_confidence.b37.vcf.idx.gz
|--Broad.human.exome.b37.interval_list.gz
|--CEUTrio.HiSeq.WGS.b37.bestPractices.phased.b37.vcf.gz
   CEUTrio.HiSeq.WGS.b37.bestPractices.phased.b37.vcf.idx.gz

|--human_g1k_v37_decoy.fasta.gz
   human_g1k_v37_decoy.fasta.fai.gz
   human_g1k_v37_decoy.dict.gz

```

The hg19 directory differs in the following file names:

* dbsnp release 138 (this is for the UCSC reference).
* the reference is `ucsc.hg19.fasta.gz`.


## Differences between b37 and hg19
* 
* Naming conventions:
  - b37: 1-22, X, Y, MT;
  - hg19: chr1-chr22, chrX, chrY, chrM;
* Mitochondrial sequence:
  - hg19 has an older one and includes alternate loci;
  - b37 has an updated one;
* Unlocalised and unplaced sequences:
  - b37: named after their accession numbers e.g. "GL000191.1";
  - hg19: 
* Alternate loci


* It's suggested to use the extended version of b37 which includes decoy
sequences. 
  - used by the 1KG in Phase II;
  - provides better results;
  - supported by GATK and IGV;
  - compatible with all the annotations (dbSNP etc.) that are reported using
  the "b37" conventions. 

* 


**References**

* GATK download: <https://www.broadinstitute.org/gatk/download/>
* Bundle location: <https://www.broadinstitute.org/gatk/guide/article?id=1215>
* Bundle contents: <http://gatkforums.broadinstitute.org/discussion/1213/whats-in-the-resource-bundle-and-how-can-i-get-it>
* b37 vs. hg19:
  - <https://answers.dnanexus.com/p/183/>
  - <https://wiki.dnanexus.com/Scientific-Notes/human-genome>
  - <http://gatkforums.broadinstitute.org/discussion/1810/whats-the-difference-between-b37-and-hg19-resources>
