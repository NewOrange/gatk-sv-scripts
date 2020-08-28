### WGDScore
***
#### 前置step:
Module 00b.BuildWGDMatrix

#### 所用docker镜像：
ibio01:5000/epiercehoffman/sv-pipeline-qc:eph_03qc_variables-e597d85

#### 测试脚本：
测试：
```shell
set -euo pipefail
Rscript /opt/WGD/bin/scoreDosageBiases.R -z -O . /.../ref_panel_1kg_v1_2
tong_WGD_scoring_matrix_output.bed.gz /.../wgd_scoring_mask.hg38.gnomad_
v3.bed
mv WGD_scores.txt.gz ref_panel_1kg_v1_2tong_WGD_scores.txt.gz
mv WGD_score_distributions.pdf ref_panel_1kg_v1_2tong_WGD_score_distributions.pdf
```

#### 测试目录

所在目录：/home/user/zhangtong/gatksv_run/cromwell-executions/GATKSVPipelineBatch/c76f7770-cc74-4e71-a5fd-bdbf97b16bc3/call-Module00b/Module00b/8ec11479-4a39-4d1f-ab41-61c8d2a96f11/call-WGD/WGD/7fef0b34-d934-40b4-ad8f-1dd76a7edb38/call-WGDScore/execution

```xml
.
├── docker_cid
├── rc
├── ref_panel_1kg_v1_2tong_WGD_score_distributions.pdf
├── ref_panel_1kg_v1_2tong_WGD_scores.txt.gz
├── script
├── script.background
├── script.submit
├── stderr
├── stderr.background
├── stdout
└── stdout.background

0 directories, 11 files
```
#### 生成文件
```
ref_panel_1kg_v1_2tong_WGD_scores.txt.gz
ref_panel_1kg_v1_2tong_WGD_score_distributions.pdf
```