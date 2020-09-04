### MaleR1
***
#### 前置step:
+ Module00c.MakeBincovMatrix
#### 作用范围：
for Allo in Allos
#### 测试样本:
+ HG00096
+ HG00129
#### 所用docker镜像：
+ ibio01:5000/gatksv/cnmops:b3af2e3
#### 所用脚本：
HG00096（shard-0）：
```xhsell
set -euo pipefail
tabix -h /.../ref_panel_1kg_v1_2tong.bincov.bed.gz "chrX" | sed 's/Start/start/' | sed 's/Chr/chr/' | sed 's/End/end/' > bincov_chrX.bed

mv bincov_chrX.bed bincov_chrX_1.bed

EMPTY_OUTPUT_ERROR="No CNV regions in result object. Rerun cn.mops with different parameters!"
set +e
bash /opt/WGD/bin/cnMOPS_workflow.sh -S /.../GRCh38_Nmask.bed -x /.../GRCh38_Nmask.bed -r 1000 -o . -M bincov_chrX_1.bed &> cnmops.out
RC=$?
set -e
if [ ! $RC -eq 0 ]; then
  if grep -q "$EMPTY_OUTPUT_ERROR" "cnmops.out"; then
    touch calls/cnMOPS.cnMOPS.gff
  else
    echo "cnMOPS_workflow.sh returned a non-zero code that was not due to an empty call file."
    exit $RC
  fi
fi
```

#### 生成目录
所在目录：/home/user/zhangtong/gatksv_run/cromwell-executions/Module00c/c473d627-53ec-45c1-a1c2-e3d4256e0f6c/call-CNMOPSLarge/CNMOPS/bcff0cd0-072e-40c5-80b2-e4b2decbeb12/call-MaleR1/shard-0/execution
```xml
.
├── bincov_chrX_1.bed
├── calls
│   └── cnMOPS.cnMOPS.gff
├── cnMOPS.compressed_matrix.bed.gz
├── cnMOPS.compressed_matrix.bed.gz.tbi
├── cnmops.out
├── cnMOPS.raw_matrix.bed.gz
├── docker_cid
├── GFFs.list
├── rc
├── samples.list
├── script
├── script.background
├── script.submit
├── stderr
├── stderr.background
├── stdout
└── stdout.background

1 directory, 17 files
```
#### 生成文件
```
bincov_chrX_1.bed
cnMOPS.cnMOPS.gff
cnMOPS.compressed_matrix.bed.gz
cnMOPS.compressed_matrix.bed.gz.tbi
cnmops.out
cnMOPS.raw_matrix.bed.gz
```