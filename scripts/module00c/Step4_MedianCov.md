### MedianCov
***
#### 前置step:
MakeBincovMatrix
#### 测试样本:
+ HG00096
+ HG00097
#### 所用docker镜像：
Todo
#### 所用脚本：
测试：
```xhsell
cd /.../call-CalcMedCov/execution


set -euo pipefail
zcat /cromwell-executions/GATKSVPipelinePhase1/981f6726-8b5d-4d6c-9842-5cac238846f0/call-Module00c/Module00c/cc9c6767-9427-47ae-88
7a-10c621dc8083/call-MedianCov/MedianCov/cb60088a-fb1a-4345-a46f-09f310b74ada/call-CalcMedCov/inputs/302947757/ref_panel_v1.bincov
.bed.gz > ref_panel_v1_fixed.bed
Rscript /opt/WGD/bin/medianCoverage.R ref_panel_v1_fixed.bed -H ref_panel_v1_medianCov.bed
Rscript -e "x <- read.table(\"ref_panel_v1_medianCov.bed\",check.names=FALSE); xtransposed <- t(x[,c(1,2)]); write.table(xtranspos
ed,file=\"ref_panel_v1_medianCov.transposed.bed\",sep=\"\\t\",row.names=F,col.names=F,quote=F)"
```

#### 生成结果
```xml
.
│   ├── rc
│   ├── ref_panel_v1_fixed.bed
│   ├── ref_panel_v1_medianCov.bed
│   └── ref_panel_v1_medianCov.transposed.bed

```