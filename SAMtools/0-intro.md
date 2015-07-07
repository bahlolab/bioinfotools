SAMtools
========

## Introduction
SAMtools is a suite of programs for interacting with high-throughput
sequencing data. It consists of three separate repositories:

* **samtools**: Reading/writing/editing/indexing/viewing SAM/BAM/CRAM format.
* **bcftools**: Reading/writing BCF2/VCF/gVCF files and
calling/filtering/summarising SNP and short indel sequence variants.
* **htslib**: A C library for reading/writing
high-throughput sequencing data.

samtools and bcftools both use htslib internally, but these
source packages contain their own copies of
htslib so they can be built independently.

The source code is written in C and is available on GitHub (development
version) and SourceForge (released version).

## Installation
* First download the tarball from SourceForge (e.g. samtools-1.2.tar.bz2) using
curl (the -L option is used because SourceForge redirects to another location).
You can confirm that you've downloaded the right file by checking that
the MD5 hash is the same as described on the download page (click the "i" info
link):

```
curl -L "http://sourceforge.net/projects/samtools/files/samtools-1.2.tar.bz2" > samtools-1.2.tar.bz2
#curl -L "http://sourceforge.net/projects/samtools/files/bcftools-1.2.tar.bz2" > bcftools-1.2.tar.bz2
md5 samtools-1.2.tar.bz2
#md5 bcftools-1.2.tar.bz2
```

* Decompress the tarball (x-extract, v-verbose, j-compress, f-file):

```
tar -xvjf samtools-1.2.tar.bz2
#tar -xvjf bcftools-1.2.tar.bz2
```

* Go into the `samtools-1.2` folder and type `make`. This will create the
binary file `samtools`, which you need to point to when you want to run
samtools.
* In order to view the latest manual page, use `man ./samtools.1` (if you're
in the samtools directory).

In summary:

```bash
curl -L "http://sourceforge.net/projects/samtools/files/samtools-1.2.tar.bz2" > samtools-1.2.tar.bz2
md5 samtools-1.2.tar.bz2
tar -xvjf samtools-1.2.tar.bz2
cd samtools-1.2
make
man ./samtools.1
```
