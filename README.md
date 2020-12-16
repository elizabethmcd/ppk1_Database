# **ppk1** Database for Designating Clades of Accumulibacter

_Last updated: 2020-12-15_

### Database Contents 

The _ppk1_ locus has been used to delineate the population structure of 'Candidatus Accumulibacter phosphatis' into distinct clades. This repository contains _ppk1_ gene sequences from select clones and genome accessions of Accumulibacter, and a workflow for 1) identifying _ppk1_ sequences in draft assemblies of Accumulibacter and 2) classifying the specific clade a given assembly belongs to. 

- `sequences/` This directory contains FASTA-formatted files of both clone sequences (`ppk1-clone-sequences.fasta`) and _ppk1_ sequences from Accumulibacter genome accessions (`ppk1-refGenomes-coding-regions.fasta`). The clone sequences are not completely representative of all clone sequences, as studies such as Peterson et al. 2008 contain 1000s of sequences.

- `ppk1-database-info.csv` Information for each _ppk1_ sequence from either a clone or genome accession. Gives the locus tag name in the FASTA-file (not specific to the study - arbitrarily given based on re-annotation), clade designation confirmed by phylogenetic placement, and study the sequence originated from. 

- `ppk1.hmm` Hidden Markov Model (HMM) constructed from Accumulibacter-specific ppk1 sequences to search for ppk1 sequences in draft Accumulibacter assemblies. Searching for _ppk1_ genes in draft genomes based on an HMM profile is preferred over performing BLAST searches. Especially since there are plenty of Accumulibacter references from diverse clades to pull _ppk1_ genes from.  

### Workflow

## References

[1]

[2]