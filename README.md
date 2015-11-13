# **AGOUTI**: Annotated Genome Optimization Using Transcriptome Information

## Overview
AGOUTI(v0.2) uses RNAseq reads to guide genome scaffolding and improve gene annotation.

```
AGOUTI works in the following steps:
	i) read RNAseq mapping results and get reads pairs uniquely mapped to different contigs
	ii) filter reads pairs based on their mapped positions and orientations
	iii) scaffolding based on reads pairs passing step ii filtration, this step uses a modified version of RNAPATH
	iv) updating assembly and gene annotations
```

## Obtain AGOUTI

To download AGOUTI, please use git to download the most recent development version through:

    git clone git@github.com:svm-zhang/AGOUTI.git

AGOUTI is designed to be light-weight by only requiring SAMtools and python 2.7 or above.

To get the current version of the download, simply do

    python agouti.py -v

You should see, for example, something like this:

    AGOUTI v0.2

In any case, please use this version as your reference.

## Command-line interface

```
python agouti.py -h
usage: agouti.py [-h] -contig FILE -bam FILE -gff FILE -out DIR [-mnl INT] [-p STR]

Welcome to AGOUTI!

optional arguments:
	-h, --help                  show this help message and exit
	-contig             FILE    specify the initial assembly in FASTA format
	-bam                FILE    specify the RNA-seq mapping results in BAM format
	-gff                FILE    specify the predicted gene model in GFF format
    -algorithm          STR     specify the scaffolding algorith: gene or weight priority [gene]
	-outdir             DIR     specify the directory to store output files
	-p                  STR     specify the output prefix [agouti]
	-mnl                INT     minimum number of supporting joining-pairs [5]
    -nN                 INT     number of Ns put in between a pair of contigs [1000]
    -minMapQ            INT     minimum mapping quality to use [5]
    -minFracOvl         FLOAT   minimum fraction of alignment to use [0.0]
    -maxFracMismatch    FLOAT   maximum fraction of mismatch per alignment [1.0]
    -debug                      Output extra info for debug
    -overwrite                  specify to overwirte all results from previous run
    -v, --version               show program's version number and exit
```

## Example

```
samtools view test.bam | \
python agouti.py | \
-contig test.fasta | \
-bam - | \
-gff test.gff | \
-out ./test | \
-p agouti > stdout
```

## Output

```
Under test folder, you will find:
	test.agouti.fasta: scaffolded assembly in FASTA format
	test.agouti.gff3: updated gene annotations in GFF3 format
	test.scaff.paths: details on scaffolding paths
	test.join_pairs: reads pairs used for scaffolding
```

## Notes

1. only GFF file generated by AUGUSTUS currently tested
2. only BAM file generated by BWA currently tested

## Contributors

Simo Zhang
Luting Zhuo

## Support

Please report any issues or questions here on github or by email to simozhan@indiana.edu
