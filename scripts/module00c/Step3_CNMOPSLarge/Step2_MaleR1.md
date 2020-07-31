### MaleR1
***
#### 作用范围:
for Allo in Allos
#### 测试样本:
+ HG00096
+ HG00097
#### 所用docker镜像：
gatksv/cnmops:b3af2e3
#### 所用脚本：
测试：
shard-0:
```xhsell
cd /.../call-MaleR1/shard-0/execution

set -euo pipefail
GCS_OAUTH_TOKEN=`gcloud auth application-default print-access-token` \
  tabix -h /.../call-MaleR1/shard-0/inputs/1843457483/ref_panel_v1.bincov.bed.gz "c
hrX" | sed 's/Start/start/' | sed 's/Chr/chr/' | sed 's/End/end/' > bincov_chrX.bed

if [ 1 == "normal" ]; then
  mv bincov_chrX.bed bincov_chrX_1.bed
else
  awk -v sex="1" '$5==sex' /.../call-MaleR1/shard-0/inputs/-613506260/hg38_v0_sv-re
sources_ref-panel_1KG_v1_ped_1kg_ref_panel_v1.ped | cut -f2 > ids.to.include
  col=$(head -n 1 bincov_chrX.bed | tr '\t' '\n'|cat -n| grep -wf ids.to.include | awk -v ORS="," '{print $1}' | sed 's/,$//g' | sed 's:\([0
-9]\+\):$&:g')
  col_a="{print \$1,\$2,\$3,$col}"
  awk -f <(echo "$col_a") bincov_chrX.bed | tr ' ' '\t' > bincov_chrX_1.bed
fi

EMPTY_OUTPUT_ERROR="No CNV regions in result object. Rerun cn.mops with different parameters!"
set +e
bash /opt/WGD/bin/cnMOPS_workflow.sh -S /.../call-MaleR1/shard-0/inputs/-1454618493
/hg38_v0_sv-resources_resources_v1_GRCh38_Nmask.bed -x /.../call-MaleR1/shard-0/inp
uts/-1454618493/hg38_v0_sv-resources_resources_v1_GRCh38_Nmask.bed -r 1000 -o . -M bincov_chrX_1.bed &> cnmops.out
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
shard-1：
```
cd /.../call-MaleR1/shard-1/execution


set -euo pipefail
GCS_OAUTH_TOKEN=`gcloud auth application-default print-access-token` \
  tabix -h /.../shard-1/inputs/1843457483/ref_panel_v1.bincov.bed.gz "c
hrY" | sed 's/Start/start/' | sed 's/Chr/chr/' | sed 's/End/end/' > bincov_chrY.bed

if [ 1 == "normal" ]; then
  mv bincov_chrY.bed bincov_chrY_1.bed
else
  awk -v sex="1" '$5==sex' /.../call-MaleR1/shard-1/inputs/-613506260/hg38_v0_sv-re
sources_ref-panel_1KG_v1_ped_1kg_ref_panel_v1.ped | cut -f2 > ids.to.include
  col=$(head -n 1 bincov_chrY.bed | tr '\t' '\n'|cat -n| grep -wf ids.to.include | awk -v ORS="," '{print $1}' | sed 's/,$//g' | sed 's:\([0
-9]\+\):$&:g')
  col_a="{print \$1,\$2,\$3,$col}"
  awk -f <(echo "$col_a") bincov_chrY.bed | tr ' ' '\t' > bincov_chrY_1.bed
fi

EMPTY_OUTPUT_ERROR="No CNV regions in result object. Rerun cn.mops with different parameters!"
set +e
bash /opt/WGD/bin/cnMOPS_workflow.sh -S /.../call-MaleR1/shard-1/inputs/-1454618493
/hg38_v0_sv-resources_resources_v1_GRCh38_Nmask.bed -x /.../call-MaleR1/shard-1/inp
uts/-1454618493/hg38_v0_sv-resources_resources_v1_GRCh38_Nmask.bed -r 1000 -o . -M bincov_chrY_1.bed &> cnmops.out
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
#### 报错
```xshell
Loading required package: rtracklayer
Error in apply(cov[, -c(1:3)], 2, median, na.rm = T) :
  dim(X) must have a positive length
Execution halted
```