BWA
===

## Introduction
BWA (Burrows-Wheeler Aligner) is a program that aligns short reads
to long reference genomes. It consists of three algorithms, each
optimised for a particular type and length of read: BWA-backtrack, BWA-SW
and BWA-MEM. The BWA-MEM algorithm is preferred for reads with length greater
than 70 bases, since it is much faster and more accurate than the other two.
The program is written in C code and is available on GitHub (development
version) and SourceForge (released version).

## Installation
* First download the tarball from SourceForge (e.g. bwa-0.7.12.tar.bz2) using
curl (the -L option is used because SourceForge redirects to another location).
You can also confirm that you've downloaded the right thing by checking that
the MD5 hash is the same as described on the download page (click the "i" info
link):

```
curl -L "http://sourceforge.net/projects/bio-bwa/files/bwa-0.7.12.tar.bz2" > bwa-0.7.12.tar.bz2
md5 bwa-0.7.12.tar.bz2
```

* Decompress the tarball (x-extract, v-verbose, j-compress, f-file):

```
tar -xvjf bwa-0.7.12.tar.bz2
```

* Go into the `bwa-0.7.12` folder and type `make`. This will create the binary
file `bwa`, which you need to point to when you want to run BWA.
* In order to view the latest manual page, use `man ./bwa.1` (if you're in the
bwa directory).

In summary:

```bash
curl -L "http://sourceforge.net/projects/bio-bwa/files/bwa-0.7.12.tar.bz2" > bwa-0.7.12.tar.bz2
md5 bwa-0.7.12.tar.bz2
tar -xvjf bwa-0.7.12.tar.bz2
cd bwa-0.7.12.tar.bz2
make
man ./bwa.1
```

## Commands
* `index`: You first need to index the reference human genome in FASTA format.


**References**

* GitHub Development: <https://github.com/lh3/bwa>
* SourcForge Release: <http://sourceforge.net/projects/bio-bwa/>
* Manual: <http://bio-bwa.sourceforge.net/bwa.shtml>
* Tutorials: <http://2013-caltech-workshop.readthedocs.org/en/latest/bwa_mapping.html>
