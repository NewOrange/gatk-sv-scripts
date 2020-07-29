### NormalR1
***
#### 作用范围:
for Chrom in Chroms
#### 测试样本:
+ HG00096
+ HG00097
#### 所用docker镜像：
gatksv/cnmops:b3af2e3
#### 所用脚本：
测试：
shard-22:

```xhsell
cd /.../call-NormalR1/shard-21/execution


set -euo pipefail
GCS_OAUTH_TOKEN=`gcloud auth application-default print-access-token` \
  tabix -h /.../call-NormalR1/shard-21/inputs/1843457483/ref_panel_v1.bincov.bed.gz "chr
22" | sed 's/Start/start/' | sed 's/Chr/chr/' | sed 's/End/end/' > bincov_chr22.bed

if [ normal == "normal" ]; then
  mv bincov_chr22.bed bincov_chr22_normal.bed
else
  awk -v sex="normal" '$5==sex' /.../call-NormalR1/shard-21/inputs/-613506260/hg38_v0_sv
-resources_ref-panel_1KG_v1_ped_1kg_ref_panel_v1.ped | cut -f2 > ids.to.include
  col=$(head -n 1 bincov_chr22.bed | tr '\t' '\n'|cat -n| grep -wf ids.to.include | awk -v ORS="," '{print $1}' | sed 's/,$//g' | sed 's:\([
0-9]\+\):$&:g')
  col_a="{print \$1,\$2,\$3,$col}"
  awk -f <(echo "$col_a") bincov_chr22.bed | tr ' ' '\t' > bincov_chr22_normal.bed
fi

EMPTY_OUTPUT_ERROR="No CNV regions in result object. Rerun cn.mops with different parameters!"
set +e
bash /opt/WGD/bin/cnMOPS_workflow.sh -S /.../call-NormalR1/shard-21/inputs/-1454618493/h
g38_v0_sv-resources_resources_v1_GRCh38_Nmask.bed -x /.../call-NormalR1/shard-21/inputs/
-1454618493/hg38_v0_sv-resources_resources_v1_GRCh38_Nmask.bed -r 3 -o . -M bincov_chr22_normal.bed &> cnmops.out
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
Normalizing...
Error in if (is.finite(mv2m)) { : argument is of length zero
Calls: cn.mops -> normalizeChromosomes
```