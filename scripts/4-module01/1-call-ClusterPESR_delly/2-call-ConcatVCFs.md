### ConcatVCFs
***
#### 前置step:
Module01.VCFCluster
#### 测试样本:
+ HG00096
+ HG00129
#### 所用docker镜像：
ibio01:5000/gatksv/sv-base-mini:b3af2e3
#### 所用脚本：
```xhsell
set -euo pipefail
vcf-concat /.../ref_panel_1kg_v1_2tong.delly.chr1.vcf.gz /.../ref_panel_1kg_v1_2tong.delly.chr2.vcf.gz 
/.../ref_panel_1kg_v1_2tong.delly.chr3.vcf.gz 
/.../ref_panel_1kg_v1_2tong.delly.chr4.vcf.gz 
/.../ref_panel_1kg_v1_2tong.delly.chr5.vcf.gz 
/.../ref_panel_1kg_v1_2tong.delly.chr6.vcf.gz 
/.../ref_panel_1kg_v1_2tong.delly.chr7.vcf.gz 
/.../ref_panel_1kg_v1_2tong.delly.chr8.vcf.gz 
/.../ref_panel_1kg_v1_2tong.delly.chr9.vcf.gz
/.../ref_panel_1kg_v1_2tong.delly.chr10.vcf.gz /.../ref_panel_1kg_v1_2tong.delly.chr11.vcf.gz /.../ref_panel_1kg_v1_2tong.delly.chr12.vcf.gz /.../ref_panel_1kg_v1_2tong.delly.chr13.vcf.gz 
/.../ref_panel_1kg_v1_2tong.delly.chr14.vcf.gz /.../ref_panel_1kg_v1_2tong.delly.chr15.vcf.gz /.../ref_panel_1kg_v1_2tong.delly.chr16.vcf.gz
/.../ref_panel_1kg_v1_2tong.delly.chr17.vcf.gz 
/.../ref_panel_1kg_v1_2tong.delly.chr18.vcf.gz /.../ref_panel_1kg_v1_2tong.delly.chr19.vcf.gz /.../ref_panel_1kg_v1_2tong.delly.chr20.vcf.gz 
/.../ref_panel_1kg_v1_2tong.delly.chr21.vcf.gz /.../ref_panel_1kg_v1_2tong.delly.chr22.vcf.gz 
/.../ref_panel_1kg_v1_2tong.delly.chrX.vcf.gz 
/.../ref_panel_1kg_v1_2tong.delly.chrY.vcf.gz | vcf-sort -c | bgzip -c > ref_panel_1kg_v1_2tong.delly.vcf.gz;
tabix -p vcf ref_panel_1kg_v1_2tong.delly.vcf.gz;
```
#### 生成目录
所在目录：/home/user/zhangtong/gatksv_run/cromwell-executions/Module01/b645dd5f-151c-4284-a7e1-c4768000457e/call-ClusterPESR_delly/ClusterPESR/1bc8864a-d8e7-4edc-987f-1f00dde29331/call-ConcatVCFs/execution
```
.
| -- docker_cid  
| -- ref_panel_1kg_v1_2tong.delly.vcf.gz      
| -- script             
| -- script.submit  
| -- stderr.background 
| -- stdout.background
| -- rc          
| -- ref_panel_1kg_v1_2tong.delly.vcf.gz.tbi
| -- script.background
| -- stderr         
| -- stdout
```
#### 生成文件
```
ref_panel_1kg_v1_2tong.delly.vcf.gz
ref_panel_1kg_v1_2tong.delly.vcf.gz.tbi
```