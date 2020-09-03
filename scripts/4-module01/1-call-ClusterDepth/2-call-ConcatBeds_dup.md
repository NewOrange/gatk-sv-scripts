### call-ConcatBeds_dup
***
#### 前置step:
Module01.call-BedCluster_dup
#### 作用范围：
仅一次
#### 测试样本:
+ HG00096
+ HG00129
#### 所用docker镜像：
ibio01:5000/gatksv/sv-base-mini:b3af2e3
#### 所用脚本：
```xhsell
awk 'FNR==1 && NR!=1 { while (/^#chrom/) getline; } 1 {print}' /.../ref_panel_1kg_v1_2tong.DUP.chr1.bed /.../ref_panel_1kg_v1_2tong.DUP.chr2.bed /.../ref_panel_1kg_v1_2tong.DUP.chr3.bed /.../ref_panel_1kg_v1_2tong.DUP.chr4.bed /.../ref_panel_1kg_v1_2tong.DUP.chr5.bed /.../ref_panel_1kg_v1_2tong.DUP.chr6.bed /.../ref_panel_1kg_v1_2tong.DUP.chr7.bed /.../ref_panel_1kg_v1_2tong.DUP.chr8.bed /.../ref_panel_1kg_v1_2tong.DUP.chr9.bed /.../ref_panel_1kg_v1_2tong.DUP.chr10.bed /.../ref_panel_1kg_v1_2tong.DUP.chr11.bed /.../ref_panel_1kg_v1_2tong.DUP.chr12.bed /.../ref_panel_1kg_v1_2tong.DUP.chr13.bed /.../ref_panel_1kg_v1_2tong.DUP.chr14.bed /.../ref_panel_1kg_v1_2tong.DUP.chr15.bed /.../ref_panel_1kg_v1_2tong.DUP.chr16.bed /.../ref_panel_1kg_v1_2tong.DUP.chr17.bed /.../ref_panel_1kg_v1_2tong.DUP.chr18.bed /.../ref_panel_1kg_v1_2tong.DUP.chr19.bed /.../ref_panel_1kg_v1_2tong.DUP.chr20.bed /.../ref_panel_1kg_v1_2tong.DUP.chr21.bed /.../ref_panel_1kg_v1_2tong.DUP.chrX.bed /.../ref_panel_1kg_v1_2tong.DUP.chrY.bed > ref_panel_1kg_v1_2tong.DUP.bed
```
#### 生成目录
所在目录：/home/user/zhangtong/gatksv_run/cromwell-executions/Module01/b645dd5f-151c-4284-a7e1-c4768000457e/call-ClusterDepth/ClusterDepth/eff43ebe-5c8b-4257-9672-fe98be9c0f4e/call-ConcatBeds_dup/execution
```
.
| -- docker_cid  
| -- ref_panel_1kg_v1_2tong.DUP.bed
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
ref_panel_1kg_v1_2tong.DUP.bed
```