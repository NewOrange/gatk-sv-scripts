### call-BedCluster_del
***
#### 前置step:
Module00c
#### 作用范围：
for contig in contiglist
#### 测试样本:
+ HG00096
+ HG00129
#### 所用docker镜像：
ibio01:5000/cwhelan/sv-pipeline:cw_3c9d26c_single_sample_annotations
#### 所用脚本：
shard-0
```xhsell
set -euo pipefail
tabix -p bed /.../ref_panel_1kg_v1_2tong.DUP.bed.gz -r chr1 \
  -p ref_panel_1kg_v1_2ong_depth_DUP_chr1 \
  -f 0.8 \
  --merge-coordinates \
  > ref_panel_1kg_v1_2tong.DUP.chr1.preexcludelist.bed

cat <(head -1 ref_panel_1kg_v1_2tong.DUP.chr1.preexcludelist.bed) <(bedtools coverage -a ref_panel_1kg_v1_2tong.DUP.chr1.preexcludelist.bed -b /.../depth_blacklist.bed.gz | awk '$NF < 0.5' | rev | cut -f5- | rev) > ref_panel_1kg_v1_2tong.DUP.chr1.bed
```
#### 生成目录
所在目录：/home/user/zhangtong/gatksv_run/cromwell-executions/Module01/b645dd5f-151c-4284-a7e1-c4768000457e/call-ClusterDepth/ClusterDepth/eff43ebe-5c8b-4257-9672-fe98be9c0f4e/call-BedCluter_dup/shard-0/execution
```
.
| -- docker_cid  
| -- ref_panel_1kg_v1_2tong.DUP.chr1.bed
| -- script
| -- script.submit
| -- stderr.background
| -- stdout.background
| -- rc
| -- ref_panel_1kg_v1_2tong.DUP.chr1.preexcludelist.bed
| -- script.background
| -- stderr
| -- stdout
```
#### 生成文件
```
ref_panel_1kg_v1_2tong.DUP.chr1.bed
ref_panel_1kg_v1_2tong.DUP.chr1.preexcludelist.bed
```