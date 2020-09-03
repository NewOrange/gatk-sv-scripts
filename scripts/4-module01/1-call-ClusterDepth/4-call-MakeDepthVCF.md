### call-MakeDepthVCF
***
#### 前置step:
Module01.call-MakeRDTestBed
#### 作用范围：
仅一次
#### 测试样本:
+ HG00096
+ HG00129
#### 所用docker镜像：
ibio01:5000/cwhelan/sv-pipeline:cw_3c9d26c_single_sample_annotations
#### 所用脚本：
```xhsell
set -euo pipefail
cut -f5 /.../ref_panel_1kg_v1_2tong.depth.bed | sed -e '1d' -e 's/,/\n/g' | sort -u > samples.list;
svtk rdtest2vcf --contigs /.../contig.fai /.../ref_panel_1kg_v1_2tong.depth.bed
samples.list ref_panel_1kg_v1_2tong.depth.vcf.gz;
```
#### 生成目录
所在目录：/home/user/zhangtong/gatksv_run/cromwell-executions/Module01/b645dd5f-151c-4284-a7e1-c4768000457e/call-ClusterDepth/ClusterDepth/eff43ebe-5c8b-4257-9672-fe98be9c0f4e/call-MakeDepthVCF/execution
```
.
| -- docker_cid  
| -- ref_panel_1kg_v1_2tong.depth.vcf.gz
| -- script
| -- script.submit
| -- stderr.background
| -- stdout.background
| -- rc
| -- script.background
| -- ref_panel_1kg_v1_2tong.depth.vcf.gz.tbi
| -- stderr
| -- stdout
```
#### 生成文件
```
ref_panel_1kg_v1_2tong.depth.vcf.gz
ref_panel_1kg_v1_2tong.depth.vcf.gz.tbi
```