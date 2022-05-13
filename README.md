# C.elegans PDE Knockout Analysis

## Background
It is estimated that 8-15% of all crop losses ($80-100 billion annual damage) are caused by plant parasitic nematodes (roundworms). (Barker et al., 1994; Kiontke and Fitch, 2013; Nicol et al., 2011). Agricultural damage caused by nematodes primarily occurs through the root system of crops. Root-knot nematodes (RKN) are the most widespread and one of the most destructive genera of plant-parasitic nematodes causing crop damage to most of the major crops in U.S. agriculture. The availability of effective compounds for the treatment and management of animal and plant parasitic nematodes is a growing concern. In agriculture, traditional chemical approaches to killing plant parasitic nematodes (i.e., nematicides such as methyl bromide and carbamates) have serious issues because of their widespread toxicity toward vertebrate animals and the environment.

To evaluate the potential of each nematode PDE gene as a target for pharmacological intervention, we created C. elegans strains with each PDE gene [pde1, pde2, pde3, pde4, pde-5 (human PDE10), pde-6 (human PDE8)] eliminated (“knocked out”) by gene editing with CRISPR/Cas9. Genomic sequencing is completed to verify targeted gene disruptione by genome center at UNH.For this project i have verified (pde1 and pde6) knockouts.
    
# Methods
##### Whole genome sequencing of c.elegans is done at genome center,UNH.

##### Files were in fastq.gz

##### To work on this project I got access to RON.

##### I have used Joe's bash tutorial,here is the link:https://github.com/Joseph7e/MDIBL-T3-WGS-Tutorial#activate-the-genomics-environment

### Pipeline for the project

Get the data from genome center

Raw Reads:Count # of Reads

Quality Check (FASTQC)

Adapter and Quality Trimming

Read Mapping:Generate SAM/BAM files

Coverage Analysis: Using samtools

Visualized on IGV

### Command lines used for analysis-

#### Activated the genomics environment-
conda activate genomics

#### Downloaded refference genome:https://www.ncbi.nlm.nih.gov/assembly/GCF_000002985.6
sftp> put C:\Users\KRANTI\Downloads\GCF_000002985.6_WBcel235_genomic.fna

#### Counted number of raw reads-
zgrep -c '^@' Sample*/*R1*

#### Counted reads by dividing 4-
zcat Sample*/*_R1_* | wc -l

#### Adapter and Quality Trimming,Run trimmomatic/Ran Joe's wrapper script-
trim_scriptV2.sh Sample_*/*_R1_* Sample_*/*_R2_*

#### To check inside the program-
which trim_scriptV2.sh  
more /usr/local/bin/trim_scriptV2.sh

#### Run fastqc to compare with new trimmed reads to compare with the original html and the new one to see the differences (Figure.1)
-fastqc 1_S1_L002_R1_001.fastq.gz  1_S1_L002_R2_001.fastq.gz -o fastqc_raw-reads

#### Read mapping 
Index your reference genome
bwa index $fasta

#### Map the reads and construct a SAM file-
bwa mem -t 24 $fasta $forward $reverse > raw_mapped.sam

#### view the file with less 
less -S raw_mapped.sam

#### Construct a coverage table using samtools 

#### Remove sequencing reads that did not match to the assembly and convert the SAM to a BAM
samtools view -@ 24 -Sb  raw_mapped.sam  | samtools sort -@ 24 - sorted_mapped

#### Examine how many reads mapped with samtools-
samtools flagstat sorted_mapped.bam

#### Calculate per base coverage with bedtools,index the new bam file-samtools index sorted_mapped.bam
bedtools genomecov -ibam sorted_mapped.bam > coverage.out

## Fastqc report

## For Sample_1

![Raw fastqc](https://user-images.githubusercontent.com/103779987/168194324-a9f78b0a-2b65-4b00-aab7-6fccfead0494.JPG)    -Figure.1 Raw fastqc
![Trmmed fastqc](https://user-images.githubusercontent.com/103779987/168194349-8c567f58-3fb5-4481-ba98-3f1b467f1053.JPG)-Figure.1 Trimmed fastqc

## Comapared fastqc and trimmomatic
Noticed that the fastqc report 'failed' for adapter content. Trimmomatic programme used to remove the adapters with Joe's wrraper script

![Rwa_reads_1ko_2Adaptor content](https://user-images.githubusercontent.com/103779987/168314853-a1c2d355-6be5-4d95-a25f-d31393b648c4.JPG) Figure.2 Fastqc
![Trimmed_reads_1ko_Adaptor content](https://user-images.githubusercontent.com/103779987/168315037-01438a11-4338-41c6-b80a-24863ff6e878.JPG) Figure.2 Trimmomatic

# Findings
<img width="960" alt="1_ko_project" src="https://user-images.githubusercontent.com/103779987/168190781-29b67e93-cb2a-4552-82d1-d857c2017ecb.PNG">
Figure .3

I used IGV to visualize the data ( gene annotations, and per sample coverage profiles). To see the gene location I have uploaded reference genome. general feature format(gff) and .bam and bam.bai files. Samples 1 had a pde-1 knockout that resulted in ~0X coverage.

## Coverage analysis
 
##### NC_003279.8        0          173452            15072434           0.0115079

##### NC_003279.8        1          448705            15072434           0.0297699

##### NC_003279.8        2          891828            15072434           0.0591695

##### NC_003279.8        3          1292804           15072434           0.0857727

##### NC_003279.8        4          1602585           15072434           0.106326

##### NC_003279.8        5          1759873           15072434           0.116761

##### NC_003279.8        6          1754549           15072434           0.116408

##### NC_003279.8        7          1618669           15072434           0.107393

##### NC_003279.8        8          1393796           15072434           0.0924732

##### NC_003279.8        9          1133946           15072434           0.0752331

##### NC_003279.8       10          876022            15072434           0.0581208

##### NC_003279.8       11          645540            15072434           0.0428292

##### NC_003279.8       12          467348            15072434           0.0310068

##### NC_003279.8       13          326575            15072434           0.021667

##### NC_003279.8       14          222378            15072434           0.014754

##### NC_003279.8       15          146765            15072434           0.00973731





