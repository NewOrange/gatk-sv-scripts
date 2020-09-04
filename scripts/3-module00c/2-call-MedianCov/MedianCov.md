### MedianCov
***
#### 前置step:
+ Module00c.gCNVCase.MakeBincovMatrix
#### 作用范围：
仅一次
#### 测试样本:
+ HG00096
+ HG00129
#### 所用docker镜像：
+ ibio01:5000/epiercehoffman/sv-pipeline-qc:eph_03qc_variables-e597d85
#### 所用脚本：
```xhsell
set -euo pipefail
zcat /.../ref_panel_1kg_v1_2tong.bincov.bed.gz > ref_panel_1kg_v1_2tong_fixed.bed
Rscript /opt/WGD/bin/medianCoverage.R ref_panel_1kg_v1_2tong_fixed.bed -H ref_panel_1kg_v1_2tong_medianCov.bed
Rscript -e "x <- read.table(\"ref_panel_1kg_v1_2tong_medianCov.bed\",check.names=FALSE); xtransposed <- t(x[,c(1,2)]); write.table(xtransposed,file=\"ref_panel_1kg_v1_2tong
_medianCov.transposed.bed\",sep=\"\\t\",row.names=F,col.names=F,quote=F)"
```

#### 生成目录
所在目录：/home/user/zhangtong/gatksv_run/cromwell-executions/Module00c/c473d627-53ec-45c1-a1c2-e3d4256e0f6c/call-MedianCov/MedianCov/c9c14b37-609c-4185-a30c-04d7903ea354/call-CalcMedCov/execution
```xml
.
├── docker_cid
├── rc
├── ref_panel_1kg_v1_2tong_fixed.bed
├── ref_panel_1kg_v1_2tong_medianCov.bed
├── ref_panel_1kg_v1_2tong_medianCov.transposed.bed
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
ref_panel_1kg_v1_2tong_fixed.bed
ref_panel_1kg_v1_2tong_medianCov.bed
ref_panel_1kg_v1_2tong_medianCov.transposed.bed
```