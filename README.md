# Creating A Curated Database of Rumen Ciliate Protozoal 18S rRNA Gene Sequences for Metataxonomic Applications


We provide a Rumen Ciliate Protozoal 18S rRNA gene sequences database as a resource for researchers aiming to improve taxonomic resolution of protozoal communities in rumen environments.

## Note to users
When new sequence data becomes available, we will make every effort to update the database accordingly.
We also welcome user feedback on ways to improve the database, including suggestions for additional data sources that are not yet included.  

If you use this database we would appreciate you cite us as:
Lawther, K., Tapio, I., Vera-Ponce de León, A. et al. A curated database of rumen ciliate protozoal 18S rRNA gene sequences for metataxonomic applications. BMC Genom Data 27, 29 (2026). https://doi.org/10.1186/s12863-026-01420-y

## Current Release
v1.0.0.  
Release date: 11 November 2025

The curated dataset comprises 228 rumen ciliate protozoal 18S rRNA gene sequences sourced from publicly available datasets.   
Sequences were processed to remove redundancy and standardise naming.   
The final database spans 23 families, 53 genera, and 100 species, and is suitable for use in metataxonomic pipelines, including QIIME2.   

## Data acquisition

Data was acquired from the following published datasets: 

Kittelmann, S., Devente, S.R., Kirk, M.R., Seedorf, H., Dehority, B.A. and Janssen, P.H., 2015. Phylogeny of intestinal ciliates, including Charonina ventriculi, and comparison of microscopy and 18S rRNA gene pyrosequencing for rumen ciliate community structure analysis. Applied and Environmental Microbiology, 81(7), pp.2433-2444. 

Li, Z., Wang, X., Zhang, Y., Yu, Z., Zhang, T., Dai, X., Pan, X., Jing, R., Yan, Y., Liu, Y. and Gao, S., 2022. Genomic insights into the phylogeny and biomass-degrading enzymes of rumen ciliates. The ISME Journal, 16(12), pp.2775-2787. 

Park, T., Wijeratne, S., Meulia, T., Firkins, J.L. and Yu, Z., 2021. The macronuclear genome of anaerobic ciliate Entodinium caudatum reveals its biological features adapted to the distinct rumen environment. Genomics, 113(3), pp.1416-1427.

The combined raw sequences can be found in the db_curation directory:
`RumenProtozoaDBv.1.0.0.18S.rawsequences.fasta`


## 18S rRNA gene sequence extraction

To process the genomic assemblies, Barrnap v0.9 was used with default parameters and –kingdom euk, to extract ribosomal RNA genes, then those identified as 18S were selected.

## Step 1: Sample name generation

Sample names were formed by combining the unique NCBI accession numbers and the full lineage.

## Step 2: Clustering with CD-HIT

CD-HIT est was used to cluster sequences at **100% identity and 100%
length** to identify duplicates.
- Outputs:   
`RumenProtozoaDBv.1.0.0.18S_clstr`  
`RumenProtozoaDBv.1.0.0.18S.clstr`

## Step 3: Manual inspection of clusters

The .clstr file was examined and for clusters containing multiple sequences only the first sequence in the cluster was kept, as a "representative" sequence.  

-Output:  
`RumenProtozoaDBv.1.0.0.18S.clsr.xlsx`

The remaining identical sequences were flagged for removal (38 sequences in total).
The sequences that were kept then underwent 1 of 2 options regarding their lineages/names

### Where IDs differed but lineagaes were the same, the sequences were assigned a group number (groups 0-22).

    >Cluster 0	
    Keep	1641nt, >GCA_023783315.1_s1|k__Eukaryota;...;s__Polyplastron_multivesiculatum *
    Remove	1641nt, >GCA_023783355.1_s1|k__Eukaryota;...;s__Polyplastron_multivesiculatum... at +/100.00%
    Remove	1641nt, >GCA_023783375.1_s1|k__Eukaryota;...;s__Polyplastron_multivesiculatum... at +/100.00%
    Remove	1641nt, >GCA_023806905.1_s1|k__Eukaryota;...;s__Polyplastron_multivesiculatum... at +/100.00%
    Remove	1641nt, >GCA_023806955.1_s1|k__Eukaryota;...;s__Polyplastron_multivesiculatum... at +/100.00%
    Remove	1641nt, >GCA_023807025.1_s1|k__Eukaryota;...;s__Polyplastron_multivesiculatum... at +/100.00%
    Remove	1641nt, >GCA_023807125.1_s1|k__Eukaryota;...;s__Polyplastron_multivesiculatum... at +/100.00%
    Remove	1641nt, >GCA_023807285.1_s1|k__Eukaryota;...;s__Polyplastron_multivesiculatum... at +/100.00%

Kept sequence was allocated a group number and renamed from:


    >GCA_023783315.1_s1|k__Eukaryota;...;s__Polyplastron_multivesiculatum

to:

    >GCA_group0|k__Eukaryota;...;s__Polyplastron_multivesiculatum

### Case 2: Where the species name differed it was removed and generalised to `s__`

    >Cluster 14	
    Keep	1488nt, >AB535662|k__Eukaryota;...;g__Ostracodinium;s__Ostracodinium_gracile *
    Remove	1488nt, >AB536718|k__Eukaryota;...;g__Ostracodinium;s__Ostracodinium_trivesiculatum... at +/100%

Kept sequence allocated a group number and renamed from:

    >AB535662|k__Eukaryota;...;g__Ostracodinium;s__Ostracodinium_gracile

to:

    >AB_group14|k__Eukaryota;...;g__Ostracodinium;s__

All group member info, and representative sequences can be found in:
`RumenProtozoaDBv.1.0.0.18S.group_info.csv`

## Step 4: Remove the redundant sequences

-   Output:   
`RumenProtozoaDBv.1.0.0.18S.filtered_prerename.fasta`

## Step 5: Apply name changes to produce the Final RNA and DNA database files

-   Outputs:  
`RumenProtozoaDBv.1.0.0.18S.RNAsequences.fasta`  
`RumenProtozoaDBv.1.0.0.18S.DNAsequences.fasta`


## Additional files and formats

In addition to the curated 18S rRNA gene sequences, we provide several supporting files.
Taxonomy information is available as a plain text file.
The database sequence files (.fasta) and tab-delimited taxonomy file follow standard formats compatible with mothur and other sequence search and classification tools.

-   Outputs  
`RumenProtozoaDBv.1.0.0.18S.taxonomy.txt`  

We have also provide the taxoxonomy and database sequences as QIIME2 artifact files. All QIIME artifacts were produced using QIIME2 v2024.10.1 and sklearn v1.4.2. 

-   Outputs:  
`2024.10.RumenProtozoaDBv.1.0.0.18S.taxonomy.qza`  
`2024.10.RumenProtozoaDBv.1.0.0.18S.sequences.qza` 

We also provide a pre-trained Naive Bayes classifier compatible with QIIME2 and a QIIME2-formatted BLAST database.

 -   Outputs:  
`2024.10.RumenProtozoaDBv.1.0.0.18S.nb.sklearn-1.4.2.qza`  
`2024.10.RumenProtozoaDBv.1.0.0.18S.blastdb.qza`  



