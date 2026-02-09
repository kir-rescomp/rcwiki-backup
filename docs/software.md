---
title: Software
description: Software on the BMRC cluster
published: true
date: 2024-10-22T09:49:24.167Z
tags: software, module, pipelines, cgat
editor: markdown
dateCreated: 2021-06-25T15:24:31.873Z
---

# Available software

# Tabs {.tabset}
## Working with software modules

> The software on BMRC cluster is maintained using module system.
{.is-info}

> Only software prepared with a uniform toolset, such as, for example, `gompi/foss-2022b, GCC/GCCcore-12.2.0` can be loaded together at the same time. An attempt to load modules with different toolsets, for example, foss-2019a and GCCcore-10.3.0 will result in an error.  
{.is-warning}

To generate a list of all available software run the following command in the command prompt:  
  
```
module avail
```
To show all modules that include `Py` somewhere in their name:

```
module avail Py
```
To search for a specific software in the list, for example, Python versions, enter:  

```
module avail 2>&1 | tr ' ' '\n' | grep -i python
```

To load a software module, for example, Python/3.10.8-GCCcore-12.2.0 use the full name of the module:

```
module load Python/3.10.8-GCCcore-12.2.0
```

The software modules include all necessary dependencies that are needed for the software to run and they are all loaded together. 

> Loading a list of modules in a single `module load` command works considerably faster, especially for many modules, than running `module load` command for each module that needs to be loaded.
{.is-info}

For example,

```
module load BEDTools/2.30.0-GCC-12.2.0 Kent_tools/450-GCC-12.2.0 SAMtools/1.17-GCC-12.2.0 Salmon/1.10.0-GCC-12.2.0 Subread/2.0.4-GCC-12.2.0
```

works much faster than running:

```
module load BEDTools/2.30.0-GCC-12.2.0
module load Kent_tools/450-GCC-12.2.0
module load SAMtools/1.17-GCC-12.2.0
module load Salmon/1.10.0-GCC-12.2.0
module load Subread/2.0.4-GCC-12.2.0
```

To list all currently loaded modules:

```
module list
```

To remove all loaded modules (which is necessary when loading modules with different toolsets):

```
module purge
```

## Kennedy-specific software

Kennedy Institute maintains a list of software that is centrally installed on the BMRC cluster with a modern uniform toolset.

> The default toolset for Kennedy sofware stack is now `gompi/foss-2022b`, `GCC/GCCcore-12.2.0` to provide compatibility across various software in complex pipelines. These modules can be loaded together. The older software stack with `gompi/foss-2020a`, `GCC/GCCcore-9.3.0` toolset is still available, but will only be supported as required.   
{.is-warning}

### Tabs {.tabset}

#### gompi/foss-2022b/GCC/GCCcore-12.2.0

##### Bioinformatics applications

Application software for genome and sequence analysis:

<table border="1" bgcolor=#f2f2f2>
        <tr>
                <td><a href="#bamtofastq_2">bamtofastq</a></td>
                <td><a href="#bamtools_2">bamtools</a></td>
                <td><a href="#bbmap_2">bbmap</a></td>
                <td><a href="#bcftools_2">bcftools</a></td>
                <td><a href="#bedtools_2">bedtools</a></td>
                <td><a href="#bmtagger_2">bmtagger</a></td>
                <td><a href="#bowtie2_2">bowtie2</a></td>
                <td><a href="#bracken_2">bracken</a></td>
                <td><a href="#bwa_2">bwa</a></td>
                <td><a href="#cd-hit_2">cd-hit</a></td>
                <td><a href="#cellranger_2">cellranger</a></td>
                <td><a href="#diamond_2">diamond</a></td>
        </tr>
        <tr>
                <td><a href="#fastqc_2">fastqc</a></td>
                <td><a href="#gcta_2">gcta</a></td>
                <td><a href="#gffutils_2">gffutils</a></td>
                <td><a href="#hisat2_2">hisat2</a></td>
                <td><a href="#hhmer_2">hhmer</a></td>
                <td><a href="#htslib_2">htslib</a></td>
                <td><a href="#humann_2">humann</a></td>
                <td><a href="#igblast_2">igblast</a></td>
                <td><a href="#igphyml_2">igphyml</a></td>
                <td><a href="#igv_2">igv</a></td>
                <td><a href="#java-genomics-toolkit_2">java-genomics-toolkit</a></td>
                <td><a href="#kallisto_2">kallisto</a></td>
        </tr>
        <tr>
                <td><a href="#kent_tools_2">kent_tools</a></td>
                <td><a href="#kraken2_2">kraken2</a></td>
                <td><a href="#meme_2">meme</a></td>
                <td><a href="#metaphlan2_2">metaphlan2</a></td>
                <td><a href="#minimap2_2">minimap2</a></td>
                <td><a href="#mixcr_2">mixcr</a></td>
                <td><a href="#mmseqs2_2">mmseqs2</a></td>
                <td><a href="#ncbi-blast_2">ncbi-blast</a></td>
                <td><a href="#ngs_2">ngs</a></td>
                <td><a href="#ngsutils_2">ngsutils</a></td>
                <td><a href="#picard-tools_2">picard-tools</a></td>
                <td><a href="#plink_2">plink</a></td>
        </tr>
        <tr>
                <td><a href="#prodigal_2">prodigal</a></td>
                <td><a href="#regenie_2">regenie</a></td>
                <td><a href="#rmats_2">rmats</a></td>
                <td><a href="#salmon_2">salmon</a></td>
                <td><a href="#samtools_2">samtools</a></td>
                <td><a href="#seqtk_2">seqtk</a></td>
                <td><a href="#sortmerna_2">sortmerna</a></td>
                <td><a href="#spades_2">spades</a></td>
                <td><a href="#sratoolkit_2">sratoolkit</a></td>
                <td><a href="#star_2">star</a></td>
                <td><a href="#stringtie_2">stringtie</a></td>
                <td><a href="#subread_2">subread</a></td>
        </tr>
        <tr>
                <td><a href="#taxonkit_2">taxonkit</a></td>
                <td><a href="#trimgalore_2">trimgalore</a></td>
                <td><a href="#trimmomatic_2">trimmomatic</a></td>
                <td><a href="#usearch_2">usearch</a></td>
                <td><a href="#vdjtools_2">vdjtools</a></td>
          			<td colspan="7"><a></a></td>
        </tr>
</table>

##### System software

Software or software libraries that are required to compile or run various applications. These include, for example, compilers, such as gcc and language interpreters (Python, R, Java, etc). Generally, these are loaded automatically by an application software module that depends on them to run. The specific packages may need to be loaded separately for development purposes. 

<table border="1" bgcolor=#f2f2f2>
        <tr>
                <td><a href="#emacs_2">emacs</a></td>
                <td><a href="#icu_2">icu</a></td>
                <td><a href="#mpfr_2">mpfr</a></td>
                <td><a href="#netcdf_2">netcdf</a></td>
                <td><a href="#pandoc_2">pandoc</a></td>
                <td><a href="#pcre_2">pcre</a></td>
                <td><a href="#python_2">python</a></td>
                <td><a href="#python3_2">python3</a></td>
                <td><a href="#r_2">R</a></td>
                <td><a href="#perl_2">Perl</a></td>
                <td><a href="#sqlite3_2">sqlite3</a></td>
                <td><a href="#tbb_2">tbb</a></td>
        </tr>
        <tr>
                <td><a href="#texinfo_2">texinfo</a></td>
                <td><a href="#tmux_2">tmux</a></td>
          			<td colspan="10"><a></a></td>
        </tr>
</table>

##### Bioinformatics applications software description

<h6 id="bamtofastq_2"></h6>

###### bamtofastq
Tool for converting 10x BAMs produced by Cell Ranger, Space Ranger, Cell Ranger ATAC, Cell Ranger DNA, and Long Ranger back to FASTQ files that can be used as inputs to re-run analysis. The FASTQ files emitted by the tool should contain the same set of sequences that were input to the original pipeline run, although the order will not be preserved. The FASTQs will be emitted into a directory structure that is compatible with the directories created by the 'mkfastq' tool.
```
module load bamtofastq/1.3.5-x64-linux
```

<h6 id="bamtools_2"></h6>

###### bamtools
BamTools provides both a programmer's API and an end-user's toolkit for handling BAM files.
```
module load BamTools/2.5.2-GCC-12.2.0
```

<h6 id="bbmap_2"></h6>

###### bbmap
BBMap short read aligner, and other bioinformatic tools.
```
module load BBMap/39.01-GCC-12.2.0
```

<h6 id="bcftools_2"></h6>

###### bcftools
BCFtools - Reading/writing BCF2/VCF/gVCF files and calling/filtering/summarising SNP and short indel sequence variants.
```
module load BCFtools/1.17-GCC-12.2.0
```

<h6 id="bedtools_2"></h6>

###### bedtools
BEDTools: a powerful toolset for genome arithmetic. The BEDTools utilities allow one to address common genomics tasks such as finding feature overlaps and computing coverage. The utilities are largely based on four widely-used file formats: BED, GFF/GTF, VCF, and SAM/BAM.
```
module load BEDTools/2.30.0-GCC-12.2.0
```

<h6 id="bmtagger_2"></h6>

###### bmtagger
Best Match Tagger for removing human reads from metagenomics datasets
```
module load bmtagger/3.101-gompi-2022b
```

<h6 id="bowtie2_2"></h6>

###### bowtie2
Bowtie 2 is an ultrafast and memory-efficient tool for aligning sequencing reads to long reference sequences. It is particularly good at aligning reads of about 50 up to 100s or 1,000s of characters, and particularly good at aligning to relatively long (e.g. mammalian) genomes. Bowtie 2 indexes the genome with an FM Index to keep its memory footprint small: for the human genome, its memory footprint is typically around 3.2 GB. Bowtie 2 supports gapped, local, and paired-end alignment modes.
```
module load Bowtie2/2.5.1-GCC-12.2.0
```

<h6 id="bracken_2"></h6>

###### bracken
Bracken (Bayesian Reestimation of Abundance with KrakEN) is a highly accurate statistical method that computes the abundance of species in DNA sequences from a metagenomics sample. Braken uses the taxonomy labels assigned by Kraken, a highly accurate metagenomics classification algorithm, to estimate the number of reads originating from each species present in a sample. Kraken classifies reads to the best matching location in the taxonomic tree, but does not estimate abundances of species. We use the Kraken database itself to derive probabilities that describe how much sequence from each genome is identical to other genomes in the database, and combine this information with the assignments for a particular sample to estimate abundance at the species level, the genus level, or above. Combined with the Kraken classifier, Bracken produces accurate species- and genus-level abundance estimates even when a sample contains two or more near-identical species. NOTE: Bracken is compatible with both Kraken 1 and Kraken 2. However, the default kmer length is different depending on the version of Kraken used.
```
module load Bracken/2.9-GCCcore-12.2.0
```

<h6 id="bwa_2"></h6>

###### bwa
Burrows-Wheeler Aligner (BWA) is an efficient program that aligns relatively short nucleotide sequences against a long reference sequence such as the human genome.
```
module load BWA/0.7.17-GCCcore-12.2.0
```

<h6 id="cd-hit_2"></h6>

###### cd-hit
CD-HIT is a very widely used program for clustering and comparing protein or nucleotide sequences.
```
module load CD-HIT/4.8.1-GCC-12.2.0
```

<h6 id="cellranger_2"></h6>

###### cellranger
Cell Ranger is a set of analysis pipelines that process Chromium single-cell RNA-seq output to align reads, generate gene-cell matrices and perform clustering and gene expression analysis.
```
module load CellRanger/7.1.0
```

<h6 id="diamond_2"></h6>

###### diamond
Accelerated BLAST compatible local sequence aligner.
```
module load DIAMOND/2.1.8-GCC-12.2.0
```

<h6 id="fastqc_2"></h6>

###### fastqc
FastQC is a quality control application for high throughput sequence data. It reads in sequence data in a variety of formats and can either provide an interactive application to review the results of several different QC checks, or create an HTML based report which can be integrated into a pipeline.
```
module load FastQC/0.11.9-Java-11
```

<h6 id="gcta_2"></h6>

###### gcta
GCTA (Genome-wide Complex Trait Analysis) was initially designed to estimate the proportion of phenotypic variance explained by all genome-wide SNPs for complex traits (i.e., the GREML method). It has been subsequently extended for many other analyses to better understand the genetic architecture of complex traits.
```
module load GCTA/1.93.2b
```

<h6 id="gffutils_2"></h6>

###### gffutils
Gffutils is a Python package for working with and manipulating the GFF and GTF format files typically used for genomic annotations.
```
module load gffutils/0.12-foss-2022b
```

<h6 id="hisat2_2"></h6>

###### hisat2
HISAT2 is a fast and sensitive alignment program for mapping next-generation sequencing reads (both DNA and RNA) against the general human population (as well as against a single reference genome).
```
module load HISAT2/2.2.1-gompi-2022b
```

<h6 id="hhmer_2"></h6>

###### hhmer
HMMER is used for searching sequence databases for homologs of protein sequences, and for making protein sequence alignments. It implements methods using probabilistic models called profile hidden Markov models (profile HMMs).  Compared to BLAST, FASTA, and other sequence alignment and database search tools based on older scoring methodology, HMMER aims to be significantly more accurate and more able to detect remote homologs because of the strength of its underlying mathematical models. In the past, this strength came at significant computational expense, but in the new HMMER3 project, HMMER is now essentially as fast as BLAST.
```
module load HMMER/3.3.2-gompi-2022b
```

<h6 id="htslib_2"></h6>

###### htslib
A C library for reading/writing high-throughput sequencing data. This package includes the utilities bgzip and tabix
```
module load HTSlib/1.17-GCC-12.2.0
```

<h6 id="humann_2"></h6>

###### humann
HUMAnN v3 is a pipeline for efficiently and accurately determining the coverage and abundance of microbial pathways in a community from metagenomic data. Sequencing a metagenome typically produces millions of short DNA/RNA reads. This process, referred to as functional profiling, aims to describe the metabolic potential of a microbial community and its members. More generally, functional profiling answers the question: What are the microbes in my community-of-interest doing (or capable of doing)?
```
module load humann/3.8-foss-2022b-Python-3.10.8
```

<h6 id="igblast_2"></h6>

###### igblast
IgBLAST faclilitates the analysis of immunoglobulin and T cell receptor variable domain sequences.
```
module load IgBLAST/1.17.0-x64-linux
```

<h6 id="igphyml_2"></h6>

###### igphyml
IgPhyML is a phylogenetic inference package for B cell repertoires. It implements codon substitution models designed that incorporate unique features of somatic hypermutation and allow for parameter estimation across lineages to characterize entire repertoires.
```
module load igphyml/2.0.0-GCC-12.2.0
```

<h6 id="igv_2"></h6>

###### igv
This package contains command line utilities for preprocessing, computing feature count density (coverage),  sorting, and indexing data files.
```
module load IGV/2.8.0-Java-11
```

<h6 id="java-genomics-toolkit_2"></h6>

###### java-genomics-toolkit
Collection of scripts for working with Wiggle files and analyzing sequencing data.
```
module load java-genomics-toolkit/0.0
```

<h6 id="kallisto_2"></h6>

###### kallisto
Kallisto is a program for quantifying abundances of transcripts from RNA-Seq data, or more generally of target sequences using high-throughput sequencing reads.
```
module load kallisto/0.48.0-gompi-2022b
```

<h6 id="kent_tools_2"></h6>

###### kent_tools
Kent utilities: collection of tools used by the UCSC genome browser.
```
module load Kent_tools/450-GCC-12.2.0
```

<h6 id="kraken2_2"></h6>

###### kraken2
Kraken 2 is the newest version of Kraken, a taxonomic classification system using exact k-mer matches to achieve high accuracy and fast classification speeds. This classifier matches each k-mer within a query sequence to the lowest common ancestor (LCA) of all genomes containing the given k-mer. The k-mer assignments inform the classification algorithm. Kraken 2 provides significant improvements to Kraken 1, with faster database build times, smaller database sizes, and faster classification speeds.
```
module load Kraken2/2.1.2-gompi-2022b
```

<h6 id="meme_2"></h6>

###### meme
The MEME Suite allows you to: * discover motifs using MEME, DREME (DNA only) or GLAM2 on groups of related DNA or protein sequences, * search sequence databases with motifs using MAST, FIMO, MCAST or GLAM2SCAN, * compare a motif to all motifs in a database of motifs, * associate motifs with Gene Ontology terms via their putative target genes, and * analyse motif enrichment using SpaMo or CentriMo.
```
module load MEME/5.4.1-gompi-2022b
```

<h6 id="metaphlan2_2"></h6>

###### metaphlan2
MetaPhlAn is a computational tool for profiling the composition of microbial communities (Bacteria, Archaea, Eukaryotes and Viruses) from metagenomic shotgun sequencing data (i.e. not 16S) with species-level. With the newly added StrainPhlAn module, it is now possible to perform accurate strain-level microbial profiling.
```
module load MetaPhlAn/4.0.6-foss-2022b
```

<h6 id="minimap2_2"></h6>

###### minimap2
Minimap2 is a fast sequence mapping and alignment program that can find overlaps between long noisy reads, or map long reads or their assemblies to a reference genome optionally with detailed alignment (i.e. CIGAR). At present, it works efficiently with query sequences from a few kilobases to ~100 megabases in length at an error rate ~15%. Minimap2 outputs in the PAF or the SAM format. On limited test data sets, minimap2 is over 20 times faster than most other long-read aligners. It will replace BWA-MEM for long reads and contig alignment.
```
module load minimap2/2.26-GCCcore-12.2.0
```

<h6 id="mixcr_2"></h6>

###### mixcr
MiXCR is a universal framework that processes big immunome data from raw sequences to quantitated clonotypes. MiXCR efficiently handles paired- and single-end reads, considers sequence quality, corrects PCR errors and identifies germline hypermutations. The software supports both partial- and full-length profiling and employs all available RNA or DNA information, including sequences upstream of V and downstream of J gene segments.
```
module load MiXCR/4.5.0-Java-11
```

<h6 id="mmseqs2_2"></h6>

###### mmseqs2
MMseqs2: ultra fast and sensitive search and clustering suite.
```
module load MMseqs2/14-7e284-gompi-2022b
```

<h6 id="ncbi-blast_2"></h6>

###### ncbi-blast
Basic Local Alignment Search Tool, or BLAST, is an algorithm for comparing primary biological sequence information, such as the amino-acid sequences of different proteins or the nucleotides of DNA sequences.
```
module load BLAST+/2.14.0-gompi-2022b
```

<h6 id="ngs_2"></h6>

###### ngs
NGS is a new, domain-specific API for accessing reads, alignments and pileups produced from Next Generation Sequencing.
```
module load NGS/2.11.2-GCCcore-12.2.0
```

<h6 id="ngsutils_2"></h6>

###### ngsutils
NGSUtils is a suite of software tools for working with next-generation sequencing datasets.
```
module load ngsutils/0.5.9
```

<h6 id="picard-tools_2"></h6>

###### picard-tools
A set of tools (in Java) for working with next generation sequencing data in the BAM format.
```
module load picard/2.25.1-Java-11
```

<h6 id="plink_2"></h6>

###### plink
Whole-genome association analysis toolset.
```
module load PLINK/2.00a3.7-foss-2022b
```

<h6 id="prodigal_2"></h6>

###### prodigal
Prodigal (Prokaryotic Dynamic Programming Genefinding Algorithm) is a microbial (bacterial and archaeal) gene finding program developed at Oak Ridge National Laboratory and the University of Tennessee.
```
module load prodigal/2.6.3-GCCcore-12.2.0
```

<h6 id="regenie_2"></h6>

###### regenie
Regenie is a C++ program for whole genome regression modelling of large genome-wide association studies. It is developed and supported by a team of scientists at the Regeneron Genetics Center.
```
module load regenie/3.2.6
```

<h6 id="rmats_2"></h6>

###### rmats
rMATS turbo is the C/Cython version of rMATS (refer to http://rnaseq-mats.sourceforge.net).
```
module load rMATS-turbo/4.2.0-foss-2022b
```

<h6 id="salmon_2"></h6>

###### salmon
Salmon is a wicked-fast program to produce a highly-accurate, transcript-level quantification estimates from RNA-seq data.
```
module load Salmon/1.10.0-GCC-12.2.0
```

<h6 id="samtools_2"></h6>

###### samtools
SAM Tools provide various utilities for manipulating alignments in the SAM format, including sorting, merging, indexing and generating alignments in a per-position format.
```
module load SAMtools/1.17-GCC-12.2.0
```

<h6 id="seqtk_2"></h6>

###### seqtk
Seqtk is a fast and lightweight tool for processing sequences in the FASTA or FASTQ format. It seamlessly parses both FASTA and FASTQ files which can also be optionally compressed by gzip.
```
module load seqtk/1.4-GCC-12.2.0
```

<h6 id="sortmerna_2"></h6>

###### sortmerna
SortMeRNA is a biological sequence analysis tool for filtering, mapping and OTU-picking NGS reads.
```
module load SortMeRNA/4.3.4
```

<h6 id="spades_2"></h6>

###### spades
Genome assembler for single-cell and isolates data sets.
```
module load SPAdes/3.15.4-GCC-12.2.0
```

<h6 id="sratoolkit_2"></h6>

###### sratoolkit
The SRA Toolkit, and the source-code SRA System Development Kit (SDK), will allow you to programmatically access data housed within SRA and convert it from the SRA format.
```
module load SRA-Toolkit/3.0.5-gompi-2022b
```

<h6 id="star_2"></h6>

###### star
STAR aligns RNA-seq reads to a reference genome using uncompressed suffix arrays.
```
module load STAR/2.7.10b-GCC-12.2.0
```

<h6 id="stringtie_2"></h6>

###### stringtie
StringTie is a fast and highly efficient assembler of RNA-Seq alignments into potential transcripts.
```
module load StringTie/2.2.1-GCC-12.2.0
```

<h6 id="subread_2"></h6>

###### subread
High performance read alignment, quantification and mutation discovery.
```
module load Subread/2.0.4-GCC-12.2.0
```

<h6 id="taxonkit_2"></h6>

###### taxonkit
A Practical and Efficient NCBI Taxonomy Toolkit.
```
module load taxonkit/0.14.2
```

<h6 id="trimgalore_2"></h6>

###### trimgalore
Trim Galore is a wrapper around Cutadapt and FastQC to consistently apply adapter and quality trimming to FastQ files, with extra functionality for RRBS data.
```
module load Trim_Galore/0.6.10-GCCcore-12.2.0
```

<h6 id="trimmomatic_2"></h6>

###### trimmomatic
Trimmomatic performs a variety of useful trimming tasks for illumina paired-end and single ended data.The selection of trimming steps and their associated parameters are supplied on the command line.
```
module load Trimmomatic/0.39-Java-11
```

<h6 id="usearch_2"></h6>

###### usearch
USEARCH is a unique sequence analysis tool which offers search and clustering algorithms that are often orders of magnitude faster than BLAST.
```
module load USEARCH/11.0.667-i86linux32
```

<h6 id="vdjtools_2"></h6>

###### vdjtools
VDJtools is an open-source Java/Groovy-based framework designed to facilitate analysis of immune repertoire sequencing (RepSeq) data. VDJtools computes a wide set of statistics and is able to perform various forms of cross-sample analysis. Both comprehensive tabular output and publication-ready plots are provided.
```
module load vdjtools/1.2.1
```

##### System software description

<h6 id="emacs_2"></h6>

###### emacs
GNU Emacs is an extensible, customizable text editor--and more. At its core is an interpreter for Emacs Lisp, a dialect of the Lisp programming language with extensions to support text editing.
```
module load Emacs/28.2-GCCcore-12.2.0
```

<h6 id="icu_2"></h6>

###### icu
ICU is a mature, widely used set of C/C++ and Java libraries providing Unicode and Globalization support for software applications.
```
module load ICU/72.1-GCCcore-12.2.0
```

<h6 id="mpfr_2"></h6>

###### mpfr
The MPFR library is a C library for multiple-precision floating-point computations with correct rounding.
```
module load MPFR/4.2.0-GCCcore-12.2.0
```

<h6 id="netcdf_2"></h6>

###### netcdf
NetCDF (network Common Data Form) is a set of software libraries and machine-independent data formats that support the creation, access, and sharing of array-oriented scientific data.
```
module load netCDF/4.9.0-gompi-2022b
```

<h6 id="pandoc_2"></h6>

###### pandoc
If you need to convert files from one markup format into another, pandoc is your swiss-army knife.
```
module load Pandoc/2.13
```

<h6 id="pcre_2"></h6>

###### pcre
The PCRE library is a set of functions that implement regular expression pattern matching using the same syntax and semantics as Perl 5.
```
module load PCRE/8.45-GCCcore-12.2.0
```

<h6 id="python_2"></h6>

###### python
Python 2
```
module load Python/2.7.18-GCCcore-12.2.0-bare
```

<h6 id="python3_2"></h6>

###### python3
Python 3
```
module load Python/3.10.8-GCCcore-12.2.0
```

<h6 id="r_2"></h6>

###### R
R 4.3.1
```
module load R/4.3.1-foss-2022b-bare
```

<h6 id="perl_2"></h6>

###### perl
Perl 5.36.0
```
module load Perl/5.36.0-GCCcore-12.2.0
```

<h6 id="sqlite3_2"></h6>

###### sqlite3
SQLite: SQL Database Engine in a C Library.
```
module load SQLite/3.39.4-GCCcore-12.2.0
```

<h6 id="tbb_2"></h6>

###### tbb
Intel(R) Threading Building Blocks (Intel(R) TBB) lets you easily write parallel C++ programs that take full advantage of multicore performance, that are portable, composable and have future-proof scalability.
```
module load tbb/2021.10.0-GCCcore-12.2.0
```

<h6 id="texinfo_2"></h6>

###### texinfo
Texinfo is the official documentation format of the GNU project.
```
module load texinfo/7.1-GCCcore-12.2.0
```

<h6 id="tmux_2"></h6>

###### tmux
Tmux is a terminal multiplexer: it enables a number of terminals to be created, accessed, and controlled from a single screen. Tmux may be detached from a screen and continue running in the background, then later reattached.
```
module load tmux/3.3a-GCCcore-12.2.0
```

#### gompi/foss-2020a/GCC/GCCcore-9.3.0

##### Bioinformatics applications

Application software for genome and sequence analysis:

<table border="1" bgcolor=#f2f2f2>
        <tr>
                <td><a href="#bamtofastq">bamtofastq</a></td>
                <td><a href="#bcftools">bcftools</a></td>
                <td><a href="#bedtools2">bedtools2</a></td>
                <td><a href="#blat">blat</a></td>
                <td><a href="#bolt-lmm">bolt-lmm</a></td>
                <td><a href="#bowtie">bowtie</a></td>
                <td><a href="#bowtie2">bowtie2</a></td>
                <td><a href="#bracken">bracken</a></td>
                <td><a href="#bustools">bustools</a></td>
                <td><a href="#bwa">bwa</a></td>
                <td><a href="#cd-hit">cd-hit</a></td>
                <td><a href="#cellranger">cellranger</a></td>
        </tr>
        <tr>
                <td><a href="#cpat">cpat</a></td>
                <td><a href="#cramtools">cramtools</a></td>
                <td><a href="#demuxlet">demuxlet</a></td>
                <td><a href="#diamond">diamond</a></td>
                <td><a href="#eggnog-mapper">eggnog-mapper</a></td>
                <td><a href="#exonerate">exonerate</a></td>
                <td><a href="#fastq_screen">fastq_screen</a></td>
                <td><a href="#fastqc">fastqc</a></td>
                <td><a href="#fastx_toolkit">fastx_toolkit</a></td>
                <td><a href="#gcta">gcta</a></td>
                <td><a href="#gffcompare">gffcompare</a></td>
                <td><a href="#gffread">gffread</a></td>
        </tr>
        <tr>
                <td><a href="#htslib">htslib</a></td>
                <td><a href="#idba">idba</a></td>
                <td><a href="#idemp">idemp</a></td>
                <td><a href="#igblast">igblast</a></td>
                <td><a href="#igraph">igraph</a></td>
                <td><a href="#igv">igv</a></td>
                <td><a href="#java-genomics-toolkit">java-genomics-toolkit</a></td>
                <td><a href="#kallisto">kallisto</a></td>
                <td><a href="#kraken">kraken</a></td>
                <td><a href="#kraken2">kraken2</a></td>
                <td><a href="#megahit">megahit</a></td>
                <td><a href="#meme">meme</a></td>
        </tr>
        <tr>
                <td><a href="#metaphlan2">metaphlan2</a></td>
                <td><a href="#minimap2">minimap2</a></td>
                <td><a href="#mixcr">mixcr</a></td>
                <td><a href="#mmseqs2">mmseqs2</a></td>
                <td><a href="#Mzmine">Mzmine</a></td>
                <td><a href="#ncbi-blast">ncbi-blast</a></td>
                <td><a href="#ngs">ngs</a></td>
                <td><a href="#ngsutils">ngsutils</a></td>
                <td><a href="#picard-tools">picard-tools</a></td>
                <td><a href="#plink">plink</a></td>
                <td><a href="#primer3">primer3</a></td>
                <td><a href="#prodigal">prodigal</a></td>
        </tr>
        <tr>
                <td><a href="#regenie">regenie</a></td>
                <td><a href="#salmon">salmon</a></td>
                <td><a href="#samtools">samtools</a></td>
                <td><a href="#seqtk">seqtk</a></td>
                <td><a href="#sortmerna">sortmerna</a></td>
                <td><a href="#spades">spades</a></td>
                <td><a href="#sratoolkit">sratoolkit</a></td>
                <td><a href="#star">star</a></td>
                <td><a href="#stringtie">stringtie</a></td>
                <td><a href="#subread">subread</a></td>
                <td><a href="#taxonkit">taxonkit</a></td>
                <td><a href="#trimgalore">trimgalore</a></td>
        </tr>
        <tr>
                <td><a href="#trimmomatic">trimmomatic</a></td>
                <td><a href="#usearch">usearch</a></td>
                <td><a href="#vdjtools">vdjtools</a></td>
                <td colspan="9"><a></a></td>         
        </tr>
</table>

##### System software

Software or software libraries that are required to compile or run various applications. These include, for example, compilers, such as gcc and language interpreters (Python, R, Java, etc). Generally, these are loaded automatically by an application software module that depends on them to run. The specific packages may need to be loaded separately for development purposes. 


<table border="1" bgcolor=#f2f2f2>
        <tr>
                <td><a href="#matlab">matlab</a></td>
                <td><a href="#mercurial">mercurial</a></td>
                <td><a href="#mpc">mpc</a></td>
                <td><a href="#mpfr">mpfr</a></td>
                <td><a href="#netcdf">netcdf</a></td>
                <td><a href="#pandoc">pandoc</a></td>
                <td><a href="#patchelf">patchelf</a></td>
                <td><a href="#pcre">pcre</a></td>
                <td><a href="#python3">python3</a></td>
                <td><a href="#r">R</a></td>
                <td><a href="#sqlite3">sqlite3</a></td>
                <td><a href="#tbb">tbb</a></td>
        </tr>
        <tr>
                <td><a href="#texinfo">texinfo</a></td>
                <td colspan="11"><a></a></td>
  			</tr>
</table>

##### Bioinformatics applications software description

###### bamtofastq
Tool for converting 10x BAMs produced by Cell Ranger, Space Ranger, Cell Ranger ATAC, Cell Ranger DNA, and Long Ranger back to FASTQ files that can be used as inputs to re-run analysis. The FASTQ files emitted by the tool should contain the same set of sequences that were input to the original pipeline run, although the order will not be preserved. The FASTQs will be emitted into a directory structure that is compatible with the directories created by the 'mkfastq' tool.
```
module load bamtofastq/1.3.5-x64-linux
```

###### bcftools
BCFtools - Reading/writing BCF2/VCF/gVCF files and calling/filtering/summarising SNP and short indel sequence variants.
```
module load BCFtools/1.12-GCC-9.3.0
```

###### bedtools2
BEDTools: a powerful toolset for genome arithmetic. The BEDTools utilities allow one to address common genomics tasks such as finding feature overlaps and computing coverage. The utilities are largely based on four widely-used file formats: BED, GFF/GTF, VCF, and SAM/BAM.
```
module load BEDTools/2.29.2-GCC-9.3.0
```

###### blat
BLAT on DNA is designed to quickly find sequences of 95% and greater similarity of length 25 bases or more.
```
module load BLAT/3.5-GCC-9.3.0
```

###### bolt-lmm
The BOLT-LMM software package currently consists of two main algorithms, the BOLT-LMM algorithm for mixed model association testing, and the BOLT-REML algorithm for variance components analysis (i.e., partitioning of SNP-heritability and estimation of genetic correlations).
```
module load BOLT-LMM/2.3.5
```

###### bowtie
Bowtie is an ultrafast, memory-efficient short read aligner.
```
module load Bowtie/1.2.3-GCC-9.3.0
```

###### bowtie2
Bowtie 2 is an ultrafast and memory-efficient tool for aligning sequencing reads to long reference sequences. It is particularly good at aligning reads of about 50 up to 100s or 1,000s of characters, and particularly good at aligning to relatively long (e.g. mammalian) genomes. Bowtie 2 indexes the genome with an FM Index to keep its memory footprint small: for the human genome, its memory footprint is typically around 3.2 GB. Bowtie 2 supports gapped, local, and paired-end alignment modes.
```
module load Bowtie2/2.4.1-GCC-9.3.0
```

###### bracken
Bracken (Bayesian Reestimation of Abundance with KrakEN) is a highly accurate statistical method that computes the abundance of species in DNA sequences from a metagenomics sample. Braken uses the taxonomy labels assigned by Kraken, a highly accurate metagenomics classification algorithm, to estimate the number of reads originating from each species present in a sample. Kraken classifies reads to the best matching location in the taxonomic tree, but does not estimate abundances of species. We use the Kraken database itself to derive probabilities that describe how much sequence from each genome is identical to other genomes in the database, and combine this information with the assignments for a particular sample to estimate abundance at the species level, the genus level, or above. Combined with the Kraken classifier, Bracken produces accurate species- and genus-level abundance estimates even when a sample contains two or more near-identical species. NOTE: Bracken is compatible with both Kraken 1 and Kraken 2. However, the default kmer length is different depending on the version of Kraken used.
```
module load Bracken/2.6.0-GCCcore-9.3.0
```

###### bustools
Bustools is a program for manipulating BUS files for single cell RNA-Seq datasets. It can be used to error correct barcodes, collapse  UMIs, produce gene count or transcript compatibility count matrices, and is useful for many other tasks. See the kallisto | bustools website for examples and instructions on how to use bustools as part of a single-cell RNA-seq workflow.
```
module load BUStools/0.40.0-GCCcore-9.3.0
```

###### bwa
Burrows-Wheeler Aligner (BWA) is an efficient program that aligns relatively short nucleotide sequences against a long reference sequence such as the human genome.
```
module load BWA/0.7.17-GCC-9.3.0
```

###### cd-hit
CD-HIT is a very widely used program for clustering and comparing protein or nucleotide sequences.
```
module load CD-HIT/4.8.1-GCC-9.3.0
```

###### cellranger
Cell Ranger is a set of analysis pipelines that process Chromium single-cell RNA-seq output to align reads, generate gene-cell matrices and perform clustering and gene expression analysis.
```
module load CellRanger/6.0.1
```

###### cpat
CPAT is a bioinformatics tool to predict s coding probability based on the RNA sequence characteristics. To achieve this goal, CPAT calculates scores of these 4 linguistic features from a set of known protein-coding genes and another set of non-coding genes.
```
module load CPAT/3.0.4-foss-2020a-Python-3.8.2
```

###### cramtools
CRAMTools is a set of Java tools and APIs for efficient compression of sequence read data. Although this is intended as a stable version the code is released asearly access. Parts of the CRAMTools are experimental and may not be supportedin the future.
```
module load cramtools/3.0
```

###### demuxlet
Genetic multiplexing of barcoded single cell RNA-seq.
```
module load demuxlet/20191212-foss-2020a
```

###### diamond
Accelerated BLAST compatible local sequence aligner.
```
module load DIAMOND/0.9.36-GCC-9.3.0
```

###### eggnog-mapper
EggNOG-mapper is a tool for fast functional annotation of novel sequences. It uses precomputed Orthologous Groups (OGs) and phylogenies from the EggNOG database (http://eggnog5.embl.de) to transfer functional information from fine-grained orthologs only.
```
module load eggnog-mapper/2.1.2-foss-2020a-Python-3.8.2
```

###### exonerate
Exonerate is a generic tool for pairwise sequence comparison. It allows you to align sequences using a many alignment models, using either exhaustive dynamic programming, or a variety of heuristics.
```
module load Exonerate/2.4.0-GCC-9.3.0
```

###### fastq_screen
FastQ Screen allows you to screen a library of sequences in FastQ format against a set of sequence databases so you can see if the composition of the library matches with what you expect.
```
module load FastQ_Screen/0.14.1-foss-2020a-Perl-5.30.2
```

###### fastqc
FastQC is a quality control application for high throughput sequence data. It reads in sequence data in a variety of formats and can either provide an interactive application to review the results of several different QC checks, or create an HTML based report which can be integrated into a pipeline.
```
module load FastQC/0.11.9-Java-11
```

###### fastx_toolkit
The FASTX-Toolkit is a collection of command line tools for Short-Reads FASTA/FASTQ files preprocessing.
```
module load FASTX-Toolkit/0.0.14-GCC-9.3.0
```

###### gcta
GCTA (Genome-wide Complex Trait Analysis) was initially designed to estimate the proportion of phenotypic variance explained by all genome-wide SNPs for complex traits (i.e., the GREML method). It has been subsequently extended for many other analyses to better understand the genetic architecture of complex traits.
```
module load GCTA/1.93.2b
```

###### gffcompare
GffCompare provides classification and reference annotation mapping and matching statistics for RNA-Seq assemblies (transfrags) or other generic GFF/GTF files.
```
module load GffCompare/0.11.6-GCCcore-9.3.0
```

###### gffread
GFF/GTF parsing utility providing format conversions, region filtering, FASTA sequence extraction and more.
```
module load gffread/0.11.6-GCCcore-9.3.0
```

###### htslib
A C library for reading/writing high-throughput sequencing data. This package includes the utilities bgzip and tabix
```
module load HTSlib/1.12-GCC-9.3.0
```

###### idba
IDBA-UD is a iterative De Bruijn Graph De Novo Assembler for Short Reads Sequencing data with Highly Uneven Sequencing Depth. It is an extension of IDBA algorithm. IDBA-UD also iterates from small k to a large k. In each iteration, short and low-depth contigs are removed iteratively with cutoff threshold from low to high to reduce the errors in low-depth and high-depth regions. Paired-end reads are aligned to contigs and assembled locally to generate some missing k-mers in low-depth regions. With these technologies, IDBA-UD can iterate k value of de Bruijn graph to a very large value with less gaps and less branches to form long contigs in both low-depth and high-depth regions.
```
module load IDBA-UD/1.1.3-GCC-9.3.0
```

###### idemp
Barcode demultiplex for Illumina I1, R1, R2 fastq.gz files.
```
module load idemp/latest-GCC-9.3.0
```

###### igblast
IgBLAST faclilitates the analysis of immunoglobulin and T cell receptor variable domain sequences.
```
module load IgBLAST/1.17.0-x64-linux
```

###### igraph
Igraph is a collection of network analysis tools with the emphasis on efficiency, portability and ease of use. igraph is open source and free. Igraph can be programmed in R, Python and C/C++.
```
module load igraph/0.8.2-foss-2020a
```

###### igv
This package contains command line utilities for preprocessing, computing feature count density (coverage),  sorting, and indexing data files.
```
module load IGV/2.8.0-Java-11
```

###### java-genomics-toolkit
Collection of scripts for working with Wiggle files and analyzing sequencing data.
```
module load java-genomics-toolkit/0.0
```

###### kallisto
Kallisto is a program for quantifying abundances of transcripts from RNA-Seq data, or more generally of target sequences using high-throughput sequencing reads.
```
module load kallisto/0.46.2-foss-2020a
```

###### kraken
Kraken is a system for assigning taxonomic labels to short DNA sequences, usually obtained through metagenomic studies. Previous attempts by other bioinformatics software to accomplish this task have often used sequence alignment or machine learning techniques that were quite slow, leading to the development of less sensitive but much faster abundance estimation programs. Kraken aims to achieve high sensitivity and high speed by utilizing exact alignments of k-mers and a novel classification algorithm.
```
module load Kraken/1.1.1-GCCcore-9.3.0
```

###### kraken2
Kraken 2 is the newest version of Kraken, a taxonomic classification system using exact k-mer matches to achieve high accuracy and fast classification speeds. This classifier matches each k-mer within a query sequence to the lowest common ancestor (LCA) of all genomes containing the given k-mer. The k-mer assignments inform the classification algorithm. Kraken 2 provides significant improvements to Kraken 1, with faster database build times, smaller database sizes, and faster classification speeds.
```
module load Kraken2/2.0.9-beta-gompi-2020a-Perl-5.30.2
```

###### megahit
An ultra-fast single-node solution for large and complex metagenomics assembly via succinct de Bruijn graph
```
module load MEGAHIT/1.2.9-GCCcore-9.3.0
```

###### meme
The MEME Suite allows you to: * discover motifs using MEME, DREME (DNA only) or GLAM2 on groups of related DNA or protein sequences, * search sequence databases with motifs using MAST, FIMO, MCAST or GLAM2SCAN, * compare a motif to all motifs in a database of motifs, * associate motifs with Gene Ontology terms via their putative target genes, and * analyse motif enrichment using SpaMo or CentriMo.
```
module load MEME/5.1.1-foss-2020a-Python-3.8.2
```

###### metaphlan2
MetaPhlAn is a computational tool for profiling the composition of microbial communities (Bacteria, Archaea, Eukaryotes and Viruses) from metagenomic shotgun sequencing data (i.e. not 16S) with species-level. With the newly added StrainPhlAn module, it is now possible to perform accurate strain-level microbial profiling.
```
module load MetaPhlAn2/2.7.8-foss-2020a-Python-3.8.2
```

###### minimap2
Minimap2 is a fast sequence mapping and alignment program that can find overlaps between long noisy reads, or map long reads or their assemblies to a reference genome optionally with detailed alignment (i.e. CIGAR). At present, it works efficiently with query sequences from a few kilobases to ~100 megabases in length at an error rate ~15%. Minimap2 outputs in the PAF or the SAM format. On limited test data sets, minimap2 is over 20 times faster than most other long-read aligners. It will replace BWA-MEM for long reads and contig alignment.
```
module load minimap2/2.17-GCCcore-9.3.0
```

###### mixcr
MiXCR is a universal framework that processes big immunome data from raw sequences to quantitated clonotypes. MiXCR efficiently handles paired- and single-end reads, considers sequence quality, corrects PCR errors and identifies germline hypermutations. The software supports both partial- and full-length profiling and employs all available RNA or DNA information, including sequences upstream of V and downstream of J gene segments. 
```
module load mixcr/3.0.13
```

###### mmseqs2
MMseqs2: ultra fast and sensitive search and clustering suite.
```
module load MMseqs2/10-6d92c-gompi-2020a
```

##### Mzmine
MZmine 2 is an open-source software for mass-spectrometry data processing, with the main focus on LC-MS data. 
```
module load MZmine/2.53
```

###### ncbi-blast
Basic Local Alignment Search Tool, or BLAST, is an algorithm for comparing primary biological sequence information, such as the amino-acid sequences of different proteins or the nucleotides of DNA sequences.
```
module load BLAST/2.10.1-Linux_x86_64
```

###### ngs
NGS is a new, domain-specific API for accessing reads, alignments and pileups produced from Next Generation Sequencing.
```
module load NGS/2.10.5-GCCcore-9.3.0
```

###### ngsutils
NGSUtils is a suite of software tools for working with next-generation sequencing datasets.
```
module load ngsutils/0.5.9
```

###### picard-tools
A set of tools (in Java) for working with next generation sequencing data in the BAM format.
```
module load picard/2.25.1-Java-11
```

###### plink
Whole-genome association analysis toolset.
```
module load PLINK/2.00a2.3_x86_64
```

###### primer3
Primer3 is a widely used program for designing PCR primers (PCR = 'Polymerase Chain Reaction'). PCR is an essential and ubiquitous tool in genetics and molecular biology. Primer3 can also design hybridization probes and sequencing primers.
```
module load Primer3/2.5.0-GCC-9.3.0
```

###### prodigal
Prodigal (Prokaryotic Dynamic Programming Genefinding Algorithm) is a microbial (bacterial and archaeal) gene finding program developed at Oak Ridge National Laboratory and the University of Tennessee.
```
module load prodigal/2.6.3-GCCcore-9.3.0
```

###### regenie
Regenie is a C++ program for whole genome regression modelling of large genome-wide association studies. It is developed and supported by a team of scientists at the Regeneron Genetics Center.
```
module load regenie/2.0.2
```

###### salmon
Salmon is a wicked-fast program to produce a highly-accurate, transcript-level quantification estimates from RNA-seq data.
```
module load Salmon/1.3.0-gompi-2020a
```

###### samtools
SAM Tools provide various utilities for manipulating alignments in the SAM format, including sorting, merging, indexing and generating alignments in a per-position format.
```
module load SAMtools/1.10-GCC-9.3.0
```

###### seqtk
Seqtk is a fast and lightweight tool for processing sequences in the FASTA or FASTQ format. It seamlessly parses both FASTA and FASTQ files which can also be optionally compressed by gzip.
```
module load seqtk/1.3-GCC-9.3.0
```

###### sortmerna
SortMeRNA is a biological sequence analysis tool for filtering, mapping and OTU-picking NGS reads. 
```
module load SortMeRNA/2.1-foss-2020a
```

###### spades
Genome assembler for single-cell and isolates data sets.
```
module load SPAdes/3.14.1-GCC-9.3.0-Python-3.8.2
```

###### sratoolkit
The SRA Toolkit, and the source-code SRA System Development Kit (SDK), will allow you to programmatically access data housed within SRA and convert it from the SRA format.
```
module load SRA-Toolkit/2.10.4-centos_linux64
```

###### star
STAR aligns RNA-seq reads to a reference genome using uncompressed suffix arrays.
```
module load STAR/2.7.3a-GCC-9.3.0
```

###### stringtie
StringTie is a fast and highly efficient assembler of RNA-Seq alignments into potential transcripts.
```
module load StringTie/2.1.4-GCC-9.3.0
```

###### subread
High performance read alignment, quantification and mutation discovery.
```
module load Subread/2.0.1-GCC-9.3.0
```

###### taxonkit
A Practical and Efficient NCBI Taxonomy Toolkit.
```
module load taxonkit/0.8.0
```

###### trimgalore
Trim Galore is a wrapper around Cutadapt and FastQC to consistently apply adapter and quality trimming to FastQ files, with extra functionality for RRBS data.
```
module load Trim_Galore/0.6.6-GCCcore-9.3.0-Python-3.8.2
```

###### trimmomatic
Trimmomatic performs a variety of useful trimming tasks for illumina paired-end and single ended data.The selection of trimming steps and their associated parameters are supplied on the command line.
```
module load Trimmomatic/0.39-Java-11
```

###### usearch
USEARCH is a unique sequence analysis tool which offers search and clustering algorithms that are often orders of magnitude faster than BLAST.
```
module load USEARCH/11.0.667-i86linux32
```

###### vdjtools
VDJtools is an open-source Java/Groovy-based framework designed to facilitate analysis of immune repertoire sequencing (RepSeq) data. VDJtools computes a wide set of statistics and is able to perform various forms of cross-sample analysis. Both comprehensive tabular output and publication-ready plots are provided.
```
module load vdjtools/1.2.1
```

##### System software description

###### matlab
MatLab 2021a Update4
```
module load MATLAB/2021a_Update4
```

###### mercurial
Mercurial is a free, distributed source control management tool. It efficiently handles projects of any size and offers an easy and intuitive interface.
```
module load Mercurial/5.7.1-GCCcore-9.3.0-Python-3.8.2
```

###### mpc
Description: Gnu Mpc is a C library for the arithmetic of complex numbers with arbitrarily high precision and correct rounding of the result. It extends the principles of the IEEE-754 standard for fixed precision real floating point numbers to complex numbers, providing well-defined semantics for every operation. At the same time, speed of operation at high precision is a major design goal.
```
module load MPC/1.1.0-GCC-9.3.0
```

###### mpfr
The MPFR library is a C library for multiple-precision floating-point computations with correct rounding.
```
module load MPFR/4.0.2-GCCcore-9.3.0
```

###### netcdf
NetCDF (network Common Data Form) is a set of software libraries and machine-independent data formats that support the creation, access, and sharing of array-oriented scientific data.
```
module load netCDF/4.7.4-gompi-2020a
```

###### pandoc
If you need to convert files from one markup format into another, pandoc is your swiss-army knife.
```
module load Pandoc/2.5
```

###### patchelf
PatchELF is a small utility to modify the dynamic linker and RPATH of ELF executables.
```
module load patchelf/0.12-GCCcore-9.3.0
```

###### pcre
The PCRE library is a set of functions that implement regular expression pattern matching using the same syntax and semantics as Perl 5.
```
module load PCRE/8.44-GCCcore-9.3.0
```

###### python3
Python 3
```
module load Python/3.8.2-GCCcore-9.3.0
```

###### R
R 4.0.0
```
module load R/4.0.0-foss-2020a
```

###### sqlite3
SQLite: SQL Database Engine in a C Library.
```
module load SQLite/3.31.1-GCCcore-9.3.0
```

###### tbb
Intel(R) Threading Building Blocks (Intel(R) TBB) lets you easily write parallel C++ programs that take full advantage of multicore performance, that are portable, composable and have future-proof scalability.
```
module load tbb/2020.1-GCCcore-9.3.0
```

###### texinfo
Texinfo is the official documentation format of the GNU project.
```
module load texinfo/6.7-GCCcore-9.3.0
```

## Other software on BMRC

An extensive list of available software on the BMRC cluster with a short description can be found [here](https://www.medsci.ox.ac.uk/divisional-services/support-services-1/bmrc/scientific-software-directory).

## Installation instructions for frequently used pipelines

- [Installing CGAT pipeline *How to install CGAT pipeline*](/cgat)
{.links-list}


