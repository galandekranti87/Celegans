# C.elegans PDE Knockout Analysis

## Background
It is estimated that 8-15% of all crop losses ($80-100 billion annual damage) are caused by plant parasitic nematodes (roundworms). (Barker et al., 1994; Kiontke and Fitch, 2013; Nicol et al., 2011). Agricultural damage caused by nematodes primarily occurs through the root system of crops. Root-knot nematodes (RKN) are the most widespread and one of the most destructive genera of plant-parasitic nematodes causing crop damage to most of the major crops in U.S. agriculture. The availability of effective compounds for the treatment and management of animal and plant parasitic nematodes is a growing concern. In agriculture, traditional chemical approaches to killing plant parasitic nematodes (i.e., nematicides such as methyl bromide and carbamates) have serious issues because of their widespread toxicity toward vertebrate animals and the environment.

To evaluate the potential of each nematode PDE gene as a target for pharmacological intervention, we created C. elegans strains with each PDE gene [pde1, pde2, pde3, pde4, pde-5 (human PDE10), pde-6 (human PDE8)] eliminated (“knocked out”) by gene editing with CRISPR/Cas9. Genomic sequencing is completed to verify targeted gene disruptione by genome center at UNH.For this project i have verified (pde1 and pde6) knockouts.
    
# Methods
Whole genome sequencing of c.elegans is done at genome center,UNH.
Files were in fastq.gz
To work on this project i got access to RON.

I have used Joe's bash tutorial,here is the link:https://github.com/Joseph7e/MDIBL-T3-WGS-Tutorial#activate-the-genomics-environment

Command lines used for analysis-

##Activated the genomics environment-
conda activate genomics

##Counted number of raw reads-
zgrep -c '^@' Sample*/*R1*

##Counted reads by dividing 4-
zcat Sample*/*_R1_* | wc -l

##Adapter and Quality Trimming,Run trimmomatic/Ran Joe's wrapper script-trim_scriptV2.sh Sample_*/*_R1_* Sample_*/*_R2_*

##If you want to see inside the program you can take a look-which trim_scriptV2.sh  more /usr/local/bin/trim_scriptV2.sh

##Run fastqc to compare with new trimmed reads to compare with the original html and the new one to see the differences (Figure.1)
-fastqc 1_S1_L002_R1_001.fastq.gz  1_S1_L002_R2_001.fastq.gz -o fastqc_raw-reads

# Findings
![Raw fastqc](https://user-images.githubusercontent.com/103779987/168194324-a9f78b0a-2b65-4b00-aab7-6fccfead0494.JPG)
Raw fastqc
![Trmmed fastqc](https://user-images.githubusercontent.com/103779987/168194349-8c567f58-3fb5-4481-ba98-3f1b467f1053.JPG)
Trimmed fastqc

<img width="960" alt="1_ko_project" src="https://user-images.githubusercontent.com/103779987/168190781-29b67e93-cb2a-4552-82d1-d857c2017ecb.PNG">
