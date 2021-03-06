# Free 1

## Fig 5A 재현 프로젝트
CLIP 및 ribosome density profiling에서 enrich되는 GO term 확인하기.


## Datasets
Gencode annotation (GRCm39)

35L33G CLIP library   &   ctrl RNA-seq library

siLin28a library   &   siLuc library

RPF-siLin28a library   &   RPF-siLuc library 


## Tools
featureCounts

GSEApy Biomart


## Read assignment
Use featureCounts

Gene-level counting

Ignoring multi-mapped reads


## Data processing 
Calcuate Clip-enrichment level & Ribosome-density change
```
cnts['log2_clip_enrichment'] = np.log2(   ( cnts['CLIP-35L33G.bam']/cnts['CLIP-35L33G.bam'].sum() )   /   ( cnts['RNA-control.bam']/cnts['RNA-control.bam'].sum() )   )
cnts['log2_rden_change'] = np.log2(  
    (   ( cnts['RPF-siLin28a.bam']/cnts['RPF-siLin28a.bam'].sum() ) / ( cnts['RNA-siLin28a.bam']/cnts['RNA-siLin28a.bam'].sum() )   )
    /
    (   ( cnts['RPF-siLuc.bam']/cnts['RPF-siLuc.bam'].sum() ) / ( cnts['RNA-siLuc.bam']/cnts['RNA-siLuc.bam'].sum() )   )   
    )
```
Total sum scaling

        - Using total # of successfully assigned alignments

Filter out low read counts

        - <30 raw reads in RNA-seq
        
        - <80 raw reads in RPF


## GO term mapping
GSEApy Biomart

map GO term accession & GO term name to Ensembl Gene IDs


## Statistical test
Mann-Whitney U test

    - for each GO term membership   vs   remaining genes

    - p-values were adjusted to FDRs by Benjamini-Hochberg method

Representative CLIP-enrich levels & Rden fold changes are defined as arithmetic differences 
between mean log2 levels/changes of GO term membership and others

(Refered to Table S6)



## Visualize
show only FDR < 0.05 for GO term

subset terms were omitted manually  

visualization is done using python matplotlib only

