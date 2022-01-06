# ppk1 Database for Designating Clades of Accumulibacter

_Last updated: 2022-01-06_

## Database Contents 

The _ppk1_ locus has been used to delineate the population structure of 'Candidatus Accumulibacter phosphatis' into distinct clades. This repository contains _ppk1_ gene sequences from select clones and genome accessions of Accumulibacter, and a workflow for 1) identifying _ppk1_ sequences in draft assemblies of Accumulibacter and 2) classifying the specific clade a given assembly belongs to. 

- `sequences/` This directory contains FASTA-formatted files of both clone sequences (`ppk1-clone-sequences.fasta`) and _ppk1_ sequences from Accumulibacter genome accessions (`ppk1-refGenomes-coding-regions.fasta`). Also included are common outgroup _ppk1_ sequences (`outgroup-ppk1-coding-regions.fasta`) that are used to root the tree. Currently included are _ppk1_ sequences for _Dechloromonas aromatica_ and _Rhodocyclus tenuis_. The clone sequences are not completely representative of all clone sequences, as studies such as Peterson et al. 2008 contain 100s of sequences.

- `ppk1-database-info.csv` Information for each _ppk1_ sequence from either a clone or genome accession. Gives the locus tag name in the FASTA-file (not specific to the study - arbitrarily given based on re-annotation), clade designation confirmed by phylogenetic placement, and study the sequence originated from. 

- `ppk1.hmm` Hidden Markov Model (HMM) constructed from Accumulibacter-specific ppk1 sequences to search for ppk1 sequences in draft Accumulibacter assemblies. Searching for _ppk1_ genes in draft genomes based on an HMM profile is preferred over performing BLAST searches. Especially since there are plenty of Accumulibacter references from diverse clades to pull _ppk1_ genes from.  

## Workflow

Clones were manually pulled down from Genbank. For _ppk1_ sequences from genome accessions, all genomes classified as "Accumulibacter" in NCBI were downloaded and searched for the _ppk1_ gene. _Note: NCBI currently classifies some related lineages (e.g. Proponivibrio) as Accumulibacter, and therefore the database may be affected by these sequences until the phylogeny of Accumulibacter is rectified._ These genes were then used to create an HMM profile by aligning sequences with muscle, and building an HMM profile with HMMER `build`. 

To identify and classify _ppk1_ sequences in your draft Accumulibacter assemblies, you can use the sequences as part of this database to create a phylogenetic tree. Outline of steps:  

1. Confirm which genomes are preliminarily classified as Accumulibacter. You can do this by using the GTDB-tk (although GTDB also sometimes mis-classifies genomes that probably belong to Proponivibrio as Accumulibacter, so use caution), or pulling down known Accumulibacter references and compare with genome-wide ANI. If the pairwise ANI of your draft genome and other Accumulibacter references is between ~75%-100% ANI, this probably falls between the established Accumulibacter lineage.  

2. Search for ppk1 hits using the `ppk1.hmm` With HMMER, you can search with the `hmmsearch` function using as a first-pass an e-value of 1e-50. Usually the top-scoring hit is what you want. For this you will need to search against predicted proteins of your candidate genomes. After identifying putative hits, you will need to identify the corresponding open reading frame of the protein hit to use combine with references and make a tree. As explained below, this is done because the original clone sequences used to make clade designations are impartial nucleotide sequences, and therefore a nucleotide alignment and tree is made. All reference sequences in the HMM model are complete protein sequences retrieved from genomes of Accumulibacter that have been verified using this method and by ANI comparisons.  

3. Combine your _ppk1_ open reading frame (nucleotide) sequences with the clone and genome accession references. Align with `muscle` or `mafft`. This is done because some of the clone sequences are partial, and therefore left as nucleotides. 

4. Create a phylogenetic tree in nucleotide mode. I would recommend RAxML, as a nucleotide tree with this few sequences doesn't take that long and provides more confidence than something like FastTree. In a tree viewer, root the tree at the clade where the outgroup sequences are (usually very obvious, long branches). Visualize where your sequences fall in relation to previously designated clade boundaries. Clade assignments to _ppk1_ sequences from reference genomes and clones are given in the `ppk1-database-info.csv` file. 

5. If the _ppk1_ sequence of your draft genome falls within a clade for which there is already a genome representative, these genomes should fall within 90%-100% ANI. Accumulibacter genomes not belonging to the same clade are usually closer to ~80% ANI, as the original IA and IIA references are similar only by 80% ANI. If your _ppk1_ sequence seems to fall within the tree but does not cluster well with the provided clone sequences and/or genome accessions, you will likely need to pull down more clone sequences. The largest collection of Accumulibacter-specific _ppk1_ sequences would be from Peterson et al. 2008 and Camejo et al. 2016, referenced below. 

To see an example of using the database and complete methods, see McDaniel and Moya et al. 2020 referenced below. 

## References

[1] McMahon KD, Yilmaz S, He S, Gall DL, Jenkins D, Keasling JD. 2007. Polyphosphate kinase genes from full-scale activated sludge plants. Appl Microbiol Biotechnol 77:167–173.

[2] He S, Gall DL, McMahon KD. 2007. “Candidatus accumulibacter” population structure in enhanced biological phosphorus removal sludges as revealed by polyphosphate kinase genes. Appl Environ Microbiol 73:5865–5874

[3] Peterson SB, Warnecke F, Madejska J, McMahon KD, Hugenholtz P. 2008. Environmental distribution and population biology of Candidatus Accumulibacter, a primary agent of biological phosphorus removal. Environ Microbiol 10:2692–2703.

[4] Camejo PY, Owen BR, Martirano J, Ma J, Kapoor V, Santo Domingo J, McMahon KD, Noguera DR. 2016. Candidatus Accumulibacter phosphatis clades enriched under cyclic anaerobic and microaerobic conditions simultaneously use different electron acceptors. Water Res 102:125–137

[5] McDaniel E, Moya-Flores F, Keene Beach N, Oyserman B, Kizaric M, Hoe Khor E, McMahon KD. 2020. Metabolic differentiation of co-occurring Accumulibacter clades revealed through genome-resolved metatranscriptomics. mSystems 2021.