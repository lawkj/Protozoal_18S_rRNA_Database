# Removing redundancy in ciliate 18S dataset

This is the README for the directory that contains the code and intermediary files used to get v1.0.0 of the ciliate 18S dataset.

## Data acquisition

Data was acquired from the following published datasets: 

Kittelmann, S., Devente, S.R., Kirk, M.R., Seedorf, H., Dehority, B.A. and Janssen, P.H., 2015. Phylogeny of intestinal ciliates, including Charonina ventriculi, and comparison of microscopy and 18S rRNA gene pyrosequencing for rumen ciliate community structure analysis. Applied and Environmental Microbiology, 81(7), pp.2433-2444. 

Li, Z., Wang, X., Zhang, Y., Yu, Z., Zhang, T., Dai, X., Pan, X., Jing, R., Yan, Y., Liu, Y. and Gao, S., 2022. Genomic insights into the phylogeny and biomass-degrading enzymes of rumen ciliates. The ISME Journal, 16(12), pp.2775-2787. 

Park, T., Wijeratne, S., Meulia, T., Firkins, J.L. and Yu, Z., 2021. The macronuclear genome of anaerobic ciliate Entodinium caudatum reveals its biological features adapted to the distinct rumen environment. Genomics, 113(3), pp.1416-1427.

## 18S rRNA gene sequence extraction

To process the genomic assemblies, Barrnap v0.9 was used with default parameters and –kingdom euk, to extract ribosomal RNA genes, then those identified as 18S were selected.

## Step 1: Sample name generation

Sample names were formed by combining the unique NCBI accession numbers and the full lineage.

## Step 2: Clustering with CD-HIT

CD-HIT est was used to cluster sequences at **100% identity and 100%
length** to identify duplicates.
- Output: `all_final_c1.0_s1.0.clstr.xlsx`

## Step 3: Manual inspection of clusters

The .clstr file was examined and for clusters containing multiple sequences only the first sequence in the cluster was kept, as a "representative" sequence.

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

### Case 2: Case 2: Where the species name differed it was removed and generalised to `s__`

    >Cluster 14	
    Keep	1488nt, >AB535662|k__Eukaryota;...;g__Ostracodinium;s__Ostracodinium_gracile *
    Remove	1488nt, >AB536718|k__Eukaryota;...;g__Ostracodinium;s__Ostracodinium_trivesiculatum... at +/100%

Kept sequence allocated a group number and renamed from:

    >AB535662|k__Eukaryota;...;g__Ostracodinium;s__Ostracodinium_gracile

to:

    >AB_group14|k__Eukaryota;...;g__Ostracodinium;s__


## Step 4: Remove the redundant sequences

-   Mapping file: `remove.txt`
-   Output: `ciliate_tax_ref_ID_filtered.fasta`

## Step 5: Apply name changes

-   Mapping file: `rename.txt`
-   Output: `ciliate_tax_ref_ID_v001.fasta`


## Final database files:
ciliate_tax_ref_ID_v001.fasta

Other formats will be made available soon...

Where new sequence data is published we will endure to update the database.
