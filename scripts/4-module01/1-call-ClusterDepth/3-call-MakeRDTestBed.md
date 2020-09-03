### call-MakeRDTestBed
***
#### 前置step:
Module01.call-ConcatBeds_dup

Module01.call-ConcatBeds_del

#### 作用范围：
仅一次
#### 测试样本:
+ HG00096
+ HG00129
#### 所用docker镜像：
ibio01:5000/cwhelan/sv-pipeline:cw_3c9d26c_single_sample_annotations
#### 所用脚本：
shard-0
```xhsell
set -euo pipefail
cat \
  <(python3 /opt/sv-pipeline/scripts/make_depth_rdtest_bed.py /.../ref_panel_1kg_v1_2tong.DEL.bed | sed '1d') \
  <(python3 /opt/sv-pipeline/scripts/make_depth_rdtest_bed.py /.../ref_panel_1kg_v1_2tong.DUP.bed | sed '1d') \
  | sort -k1,1V -k2,2n \
  | cat <(echo -e "#chrom start end name samples svtype" | sed -e 's/ /\t/g') - \
  > ref_panel_1kg_v1_2tong.depth.bed;
```
#### 生成目录
所在目录：/home/user/zhangtong/gatksv_run/cromwell-executions/Module01/b645dd5f-151c-4284-a7e1-c4768000457e/call-ClusterDepth/ClusterDepth/eff43ebe-5c8b-4257-9672-fe98be9c0f4e/call-MakeRDTestBed/execution
```
.
| -- docker_cid  
| -- ref_panel_1kg_v1_2tong.depth.bed
| -- script
| -- script.submit
| -- stderr.background
| -- stdout.background
| -- rc
| -- script.background
| -- stderr
| -- stdout
```
#### 生成文件
```
ref_panel_1kg_v1_2tong.depth.bed
```