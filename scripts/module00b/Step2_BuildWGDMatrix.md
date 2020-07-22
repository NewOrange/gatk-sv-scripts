### BuildWGDMatrix
***
#### 前置step:
Module 00b.Step1

#### 所用docker镜像：
Todo

#### 所用脚本：
测试：
```
​```shell
cd /cromwell-executions/Module00b/8c27f4b2-ef29-44de-8ff1-0b3759a09e8e/call-WGD/WGD/fb421920-9716-4143-8348-38ec9d0b71b6/call-BuildWGDMatrix/execution


set -eu
zcat /cromwell-executions/Module00b/8c27f4b2-ef29-44de-8ff1-0b3759a09e8e/call-WGD/WGD/fb421920-9716-4143-8348-38ec9d0b71b6/call-BuildWGDMatrix/inputs/11
51877870/test_hg00096.bincov.bed.gz | head -n 1 > header.txt
sed -i 's/#//g' header.txt

set -o pipefail
zcat /cromwell-executions/Module00b/8c27f4b2-ef29-44de-8ff1-0b3759a09e8e/call-WGD/WGD/fb421920-9716-4143-8348-38ec9d0b71b6/call-BuildWGDMatrix/inputs/11
51877870/test_hg00096.bincov.bed.gz \
| bedtools intersect -f 0.49 -wa -u \
  -a - \
  -b /cromwell-executions/Module00b/8c27f4b2-ef29-44de-8ff1-0b3759a09e8e/call-WGD/WGD/fb421920-9716-4143-8348-38ec9d0b71b6/call-BuildWGDMatrix/inputs/-1
454618493/hg38_v0_sv-resources_resources_v1_wgd_scoring_mask.hg38.gnomad_v3.bed \
| sort -Vk1,1 -k2,2n -k3,3n \
> test_hg00096_WGD_scoring_matrix.bed

cat header.txt test_hg00096_WGD_scoring_matrix.bed \
| bgzip -c \
> test_hg00096_WGD_scoring_matrix_output.bed.gz
```

#### 生成结果
```xml
.
├── docker_cid
├── header.txt
├── rc
├── script
├── script.background
├── script.submit
├── stderr
├── stderr.background
├── stdout
├── stdout.background
├── test_hg00096_WGD_scoring_matrix.bed
└── test_hg00096_WGD_scoring_matrix_output.bed.gz

0 directories, 12 files
```