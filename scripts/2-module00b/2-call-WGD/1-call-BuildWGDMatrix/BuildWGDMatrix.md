### BuildWGDMatrix
***
#### 前置step:
Module 00b.MakeBincovMatrix

#### 所用docker镜像：
ibio01:5000/epiercehoffman/sv-pipeline-qc:eph_03qc_variables-e597d85

#### 测试脚本：
测试：
```shell
set -eu
zcat /.../ref_panel_1kg_v1_2tong.bincov.bed.gz | head -n 1 > head
er.txt
sed -i 's/#//g' header.txt

set -o pipefail
zcat /.../ref_panel_1kg_v1_2tong.bincov.bed.gz \
| bedtools intersect -f 0.49 -wa -u \
  -a - \
  -b /.../wgd_scoring_mask.hg38.gnomad_v3.bed \
| sort -Vk1,1 -k2,2n -k3,3n \
> ref_panel_1kg_v1_2tong_WGD_scoring_matrix.bed

cat header.txt ref_panel_1kg_v1_2tong_WGD_scoring_matrix.bed \
| bgzip -c \
> ref_panel_1kg_v1_2tong_WGD_scoring_matrix_output.bed.gz
```

#### 测试目录

所在目录：/home/user/zhangtong/gatksv_run/cromwell-executions/GATKSVPipelineBatch/c76f7770-cc74-4e71-a5fd-bdbf97b16bc3/call-Module00b/Module00b/8ec11479-4a39-4d1f-ab41-61c8d2a96f11/call-WGD/WGD/7fef0b34-d934-40b4-ad8f-1dd76a7edb38/call-BuildWGDMatrix/execution

```xml
.
├── docker_cid
├── header.txt
├── rc
├── ref_panel_1kg_v1_2tong_WGD_scoring_matrix.bed
├── ref_panel_1kg_v1_2tong_WGD_scoring_matrix_output.bed.gz
├── script
├── script.background
├── script.submit
├── stderr
├── stderr.background
├── stdout
└── stdout.background

0 directories, 12 files
```
#### 生成文件
```
ref_panel_1kg_v1_2tong_WGD_scoring_matrix.bed
ref_panel_1kg_v1_2tong_WGD_scoring_matrix_output.bed.gz
```