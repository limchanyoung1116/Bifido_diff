## 1. _Bifidobacterium fermentum_ strain 사이의 유전적 차이 찾기

- Ilumina sequencing machine 으로 sequencing된 15개의 _Bifidobacterium fermentum_ genome들을 비교하기
- 각 genome만이 갖고 있는, 다른 genome들에는 없는 locus를 찾기
- 해당 locus에 존재하는 gene들을 찾기

### 1-1. Genome상에서 서로 다른 영역 찾기

1) Neptune program을 이용해 특징적인 영역 찾기

- 15개의 genome에 대해 각각 Neptune ingroup 1 genome, outgroup 14 genome을 수행하기
  - 특정 genome만이 갖고있고, 다른 genome들은 갖지 않는 특이한 sequence를 찾을 수 있음
  - K=22, 최소 length 배율 x4 옵션으로 실행 시 15 genome중 어느 genome에서도 특이한 서열이 존재하지 않음
  - K=13, filter 0.6(default 0.5) 으로 조정시 9개의 genome에서 특이한 서열이 발견됨

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

### 1-2. Mapping

### 1-3. 검증
