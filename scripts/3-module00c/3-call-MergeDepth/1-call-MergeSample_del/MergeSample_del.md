### MergeSample_del
***
#### 前置step:
+ Module00c.gCNVCase
+ Module00c.CNMOPS
+ Module00c.CNMOPSLarge
#### 作用范围：
for i in range(length(samples))
#### 测试样本:
+ HG00096
+ HG00129
#### 所用docker镜像：
+ ibio01:5000/cwhelan/sv-pipeline:cw_3c9d26c_single_sample_annotations
#### 所用脚本：
HG00096：
```xhsell
set -euo pipefail
zcat /.../ref_panel_1kg_v1_2tong.DEL.header.bed.gz /.../ref_panel_1kg_v1_2tong.DEL.large.bed.gz | awk -F "\t" -v OFS="\t" '{if ($5=="HG00096") print}' > cnmops.cnv
cat /.../HG00096.del.bed cnmops.cnv | sort -k1,1V -k2,2n > HG00096.bed
bedtools merge -i HG00096.bed -d 0 -c 4,5,6,7 -o distinct > HG00096.merged.bed
/opt/sv-pipeline/00_preprocessing/scripts/defragment_cnvs.py \
  --max-dist 0.25 HG00096.merged.bed HG00096.merged.defrag.bed
sort -k1,1V -k2,2n HG00096.merged.defrag.bed > HG00096.merged.defrag.sorted.bed
```

#### 生成目录
所在目录：/home/user/zhangtong/gatksv_run/cromwell-executions/Module00c/9689f669-dda1-40b4-a6df-aa35c9d84202/call-MergeDepth/MergeDepth/86744103-1c75-47aa-be83-cdcba8448706/call-MergeSample_del/shard-0/execution
```xml
.
├── cnmops.cnv
├── docker_cid
├── HG00096.bed
├── HG00096.merged.bed
├── HG00096.merged.defrag.bed
├── HG00096.merged.defrag.sorted.bed
├── rc
├── script
├── script.background
├── script.submi
├── stderr
├── stderr.background
├── stdout
└── stdout.background

0 directories, 14 files
```
#### 生成文件
```
HG00096.bed
HG00096.merged.bed
HG00096.merged.defrag.bed
HG00096.merged.defrag.sorted.bed
```