
# clean-fastq

[![Snakemake](https://img.shields.io/badge/snakemake-5.5.2-brightgreen.svg)](https://snakemake.bitbucket.io)



A workflow designed to clean fastq files for the [SEACONNECT project](https://reefish.umontpellier.fr/index.php?article9/total-seaconnect)


# Installation

## Prerequisites

* [singularity](https://github.com/sylabs/singularity)
* [snakemake](https://snakemake.bitbucket.io)

## Singularity containers

### Install Singularity
See [https://www.sylabs.io/docs/](https://www.sylabs.io/docs/) for instructions to install Singularity.

### Programs

- [fastq_illumina_filter](http://cancan.cshl.edu/labmembers/gordon/fastq_illumina_filter/) keeps reads that were NOT filtered by illumina sequencer.
- [fastp](https://github.com/OpenGene/fastp) provides fast all-in-one preprocessing for `fastq` files.
- [bbduk](https://jgi.doe.gov/data-and-tools/bbtools/) filters or trims reads for adapters and contaminants using k-mers.


### Download (or build) the container

```
singularity pull --name cleanfastq.simg ..........................
```
alternatively, if you are administrator on your machine, you can build a local image:
```
sudo singularity build cleanfastq.simg Singularity.cleanfastq
```
### Run the Obitools container

```
singularity run cleanfastq.simg
```
it should output:
```
Opening container...ubuntu xenial: fastq_illumina_filter, bbduck, fastp
```


# The pipeline 

## filter illumina fastq


## Remove adapters and contaminants

- The viral genome of phiX is used as a control in Illumina sequencing. While the viral libraries do not have MIDs on them, some phiX reads always creep through, possibly because the clusters “borrow” the signals from closely surrounding clusters that do. These phiX reads are removed.

- Adapter sequences should be removed from reads because they interfere with downstream analyses, such as alignment of reads to a reference. The adapters contain the sequencing primer binding sites, the index sequences, and the sites that allow library fragments to attach to the flow cell lawn. Illumina Truseq and Nextera adapters sequences are trimmed from reads sequence. 




# Running the pipeline

```
snakemake -s 00-scripts/snakefile -j 8 --use-singularity
```
