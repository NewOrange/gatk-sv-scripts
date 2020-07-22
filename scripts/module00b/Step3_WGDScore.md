### WGDScore
***
#### 前置step:
Module 00b.Step2

#### 所用docker镜像：
Todo

#### 所用脚本：
测试：
```shell
cd /cromwell-executions/Module00b/8c27f4b2-ef29-44de-8ff1-0b3759a09e8e/call-WGD/WGD/fb421920-9716-4143-8348-38ec9d0b71b6/call-WGDScore/execution


set -euo pipefail
Rscript /opt/WGD/bin/scoreDosageBiases.R -z -O . /cromwell-executions/Module00b/8c27f4b2-ef29-44de-8ff1-0b3759a09e8e/call-WGD/WGD/fb421920-9716-4143-834
8-38ec9d0b71b6/call-WGDScore/inputs/718412097/test_hg00096_WGD_scoring_matrix_output.bed.gz /cromwell-executions/Module00b/8c27f4b2-ef29-44de-8ff1-0b375
9a09e8e/call-WGD/WGD/fb421920-9716-4143-8348-38ec9d0b71b6/call-WGDScore/inputs/-1454618493/hg38_v0_sv-resources_resources_v1_wgd_scoring_mask.hg38.gnoma
d_v3.bed
mv WGD_scores.txt.gz test_hg00096_WGD_scores.txt.gz
mv WGD_score_distributions.pdf test_hg00096_WGD_score_distributions.pdf
```

#### 生成结果
```xml
.
├── docker_cid
├── rc
├── script
├── script.background
├── script.submit
├── stderr
├── stderr.background
├── stdout
├── stdout.background
├── test_hg00096_WGD_score_distributions.pdf
└── test_hg00096_WGD_scores.txt.gz
```