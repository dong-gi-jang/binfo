# Free 1
## Fig 5A 재현
CLIP 및 ribosome profiling에서 enrich되는 GO term 확인.


subread의 featurecounts 이용, 우선은 ignore all 방식으로 multimapping 처리한 gene level에서 GO analysis 진행 예정. 차후 transcript level에 적절한 multimapping 처리 방식 및 간단히 결과 확인해본 후 transcript에서 보아도 될지 여부 판단.

Normalize 
 - 각 실험에서의 total sum 이용한 normalze.
 - 우선은 featurecounts 결과에서의 column sum을 기반으로 normalize
 - transcript에서 진행해보려면 per read length 적용 필요??

Cutoff
 - 작은 값들끼리의 ratio 튀는 것 방지 위함, zero value 처리 위함.
 - 논문 참조, read 개수 30, 80 적용?

Statistical test
 - log2 fc of ribosome density에 대한 test
 - ttest 대신 Wilcoxon ranksum 진행

Identifier mapping
 - gseapy 이용, biomart에서 gene symbol 가져오기

GO analysis
 - gseapy 이용, enrichr에서 GO:CC,BP,MF 2021에 대한 분석

Visualize
 - pyplot scatter로 진행
