# Free 1
## Fig 5A 재현
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
featureCounts
Gene-level counting
Ignoring multi-mapped reads

## Data processing 
```
cnts['log2_clip_enrichment'] = np.log2(   ( cnts['CLIP-35L33G.bam']/cnts['CLIP-35L33G.bam'].sum() )   /   ( cnts['RNA-control.bam']/cnts['RNA-control.bam'].sum() )   )
cnts['log2_rden_change'] = np.log2(  
    (   ( cnts['RPF-siLin28a.bam']/cnts['RPF-siLin28a.bam'].sum() ) / ( cnts['RNA-siLin28a.bam']/cnts['RNA-siLin28a.bam'].sum() )   )
    /
    (   ( cnts['RPF-siLuc.bam']/cnts['RPF-siLuc.bam'].sum() ) / ( cnts['RNA-siLuc.bam']/cnts['RNA-siLuc.bam'].sum() )   )   
    )
```
Total sum scaling
Using total # of successfully assigned alignments
Filter out low read counts
<30 raw reads in RNA-seq
<80 raw reads in RPF
ript에서 진행해보려면 per read length 적용 필요??


## Statistical test
 - log2 fc of ribosome density에 대한 test
 - ttest 대신 Wilcoxon ranksum 진행

Identifier mapping
 - gseapy 이용, biomart에서 gene symbol 가져오기

GO analysis
 - gseapy 이용, enrichr에서 GO:CC,BP,MF 2021에 대한 분석

Visualize
 - pyplot scatter로 진행

