### call-ConcatBeds_del
***
#### 前置step:
Module01.call-BedCluster_del
#### 作用范围：
仅一次
#### 测试样本:
+ HG00096
+ HG00129
#### 所用docker镜像：
ibio01:5000/gatksv/sv-base-mini:b3af2e3
#### 所用脚本：
```xhsell
awk 'FNR==1 && NR!=1 { while (/^#chrom/) getline; } 1 {print}' /.../ref_panel_1kg_v1_2tong.DEL.chr1.bed /.../ref_panel_1kg_v1_2tong.DEL.chr2.bed /.../ref_panel_1kg_v1_2tong.DEL.chr3.bed /.../ref_panel_1kg_v1_2ton
g.DEL.chr4.bed /.../ref_panel_1kg_v1_2tong.DEL.chr5.bed /.../ref_panel_1kg_v1_2tong.DEL.chr6.bed /.../ref_panel_1kg_v1_2tong.DEL.chr7.bed /.../ref_panel_1kg_v1_2tong.DEL.chr8.bed /.../ref_panel_1kg_v1_2tong.DEL.chr9.bed /.../ref_panel_1kg_v1_2tong.DEL.chr10.bed /.../ref_panel_1kg_v1_2tong.DEL.chr11.bed /.../ref_panel_1kg_v1_2tong.DEL.chr12.bed /.../ref_panel_1kg_v1_2tong.DEL.chr13.bed /.../ref_panel_1kg_v1_2tong.DEL.chr14.bed /.../ref_panel_1kg_v1_2tong.DEL.chr15.bed /.../ref_panel_1kg_v1_2tong.DEL.chr16.bed /.../ref_panel_1kg_v1_2tong.DEL.chr17.bed /.../ref_panel_1kg_v1_2tong.DEL.chr18.bed /.../ref_panel_1kg_v1_2tong.DEL.chr19.bed /.../ref_panel_1kg_v1_2tong.DEL.chr20.bed /.../ref_panel_1kg_v1_2tong.DEL.chr21.bed /.../ref_panel_1kg_v1_2tong.DEL.chrX.bed /.../ref_panel_1kg_v1_2tong.DEL.chrY.bed > ref_panel_1kg_v1_2tong.DEL.bed
```
#### 生成目录
所在目录：/home/user/zhangtong/gatksv_run/cromwell-executions/Module01/b645dd5f-151c-4284-a7e1-c4768000457e/call-ClusterDepth/ClusterDepth/eff43ebe-5c8b-4257-9672-fe98be9c0f4e/call-ConcatBeds_del/execution
```
.
| -- docker_cid  
| -- ref_panel_1kg_v1_2tong.DEL.bed
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
ref_panel_1kg_v1_2tong.DEL.bed
```