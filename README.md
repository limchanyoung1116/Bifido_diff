## 1. _Bifidobacterium fermentum_ strain 사이의 유전적 차이 찾기

- Sequencing 후 assembly된 15개의 _Bifidobacterium fermentum_ genome들을 비교하기
- 각 genome만이 갖고 있는, 다른 genome들에는 없는 locus를 찾기
- 해당 locus에 존재하는 gene들을 찾기

### 1-1. Genome상에서 서로 다른 영역 찾기

1) Neptune program을 이용해 특징적인 영역 찾기

- [Neptune github](https://github.com/phac-nml/neptune)
  - Neptune은 genome들을 ingroup, outgroup들로 나누어 특정 group에서는 공유되고, 다른 특정 group에서는 존재하지 않는 genome상의 locus를 찾는 프로그램임
  - Neptune은 k-mer를 기반으로 작동하며 k 길이는 조절가능함
- 15개의 genome에 대해 각각 Neptune ingroup 1 genome, outgroup 14 genome을 수행하기
  - K=22, 최소 length 배율 x4 옵션으로 실행 시 15 genome중 어느 genome에서도 특이한 서열이 존재하지 않음
  - K=13, filter 0.6(default 0.5) 으로 조정시 9개의 genome에서 특이한 서열이 발견됨
  - 이 중 KJM407, ME3, SRP423 3개의 genome에서 유의미한 수의 contig들이 발견됨
  - 이 세 genome을 target으로 하여 mapping

|Strain|Number of sequence|average length|average score|max length|min length|score>0.7|
|---|-----|-----|-----|-----|-----|-----|
|KJM407|37|67.55|0.97|106|53|36|
|MSK408|4|58.25|0.89|85|52|4|
|ME3|69|65.53|0.95|114|52|65|
|LB12|12|72.72|0.91|120|52|11|
|KKP442|1|62|0.67|62|62|1|
|SKR310|0|0.0|0.0|0|0|0|
|SRP421|6|61.85|0.81|83|54|5|
|MSK411|1|78|0.67|78|78|1|
|K5|13|63.11|0.92|93|54|12|
|K36|0|0.0|0.0|0|0|0|
|E11|0|0.0|0.0|0|0|0|
|SJ08|0|0.0|0.0|0|0|0|
|MF27|1|61|0.47|61|61|1|
|E432I|0|0.0|0.0|0|0|0|
|SRP423|77|68.85|0.97|154|52|76|

2) bowtie2 mapping

- bowtie2 프로그램을 이용하여, Neptune output contig들을 원래 assembly genome상에 mapping
- output sam file을 살펴본 결과 대부분의 contig이 assembly genome의 여러 NODE 상에 고르게 퍼져 나타남
- contig가 두개 이상 mapping되었고, 길이가 5000 이상인 NODE들을 확인
- KJM407에서는 length 7361에 20 contig가 mapping된 NODE 50과 length 6308에 7 contig가 mapping된 NODE 54가 존재
- SRP423에서는 length 12887에 16 contig가 mapping된 NODE 39가 존재

### 1-2. 검증

1) contig 자르기
- SRP423의 NODE 39에서, 8976bp부터 12887bp 사이에 약 500~1000bp 간격으로 50~110 길이의 contig가 하나씩 존재
  - 따라서 contig들이 몰려 있는 8900bp부터 12887bp 사이 구간을 잘라냄
- KJM407의 NODE 50에서, 300bp부터 5800bp 사이 구간에 10개의 contig가 존재
  - 따라서 contig들이 몰려 있는 200bp부터 5900bp 사이 구간을 잘라냄
- KJM407의 NODE 54에서, 5400bp부터 6000bp 사이 구간에 3개의 contig가 존재
  - 따라서 5300bp부터 6100bp 사이 구간을 잘라냄
- [KJM407-NODE50, SRP423-NODE39 sequence file](https://github.com/limchanyoung1116/Bifido_diff/tree/main/genomefiles)

2) contig mapping
- 잘라낸 genome들을 bowtie2에서, 다른 14개의 genome들에 mapping 시도
  - 3개의 잘라낸 genome들 모두 어떤 genome에도 mapping되지 않음
- 잘라내지 않은 NODE39, NODE50, NODE54를 다른 14개의 genome에 다시 mapping 시도
  - 3개의 NODE 모두 어떤 genome에도 mapping되지 않음

### 1-3. 검증2 - blastn 사용

- 15개의 genome들 중 target인 SRP423과 KJM407을 제외한 13개의 genome으로 blast database 제작
  - SRP423_NODE39와 KJM407_NODE50, NODE54에 대해서 blastn query 진행
  - 일치하는 서열이 존재하지 않았음
