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
vcf-concat /.../ref_panel_1kg_v1_2tong.manta.chr1.vcf.gz /.../ref_panel_1kg_v1_2tong.manta.chr2.vcf.gz 
/.../ref_panel_1kg_v1_2tong.manta.chr3.vcf.gz 
/.../ref_panel_1kg_v1_2tong.manta.chr4.vcf.gz 
/.../ref_panel_1kg_v1_2tong.manta.chr5.vcf.gz 
/.../ref_panel_1kg_v1_2tong.manta.chr6.vcf.gz 
/.../ref_panel_1kg_v1_2tong.manta.chr7.vcf.gz 
/.../ref_panel_1kg_v1_2tong.manta.chr8.vcf.gz 
/.../ref_panel_1kg_v1_2tong.manta.chr9.vcf.gz
/.../ref_panel_1kg_v1_2tong.manta.chr10.vcf.gz /.../ref_panel_1kg_v1_2tong.manta.chr11.vcf.gz /.../ref_panel_1kg_v1_2tong.manta.chr12.vcf.gz /.../ref_panel_1kg_v1_2tong.manta.chr13.vcf.gz 
/.../ref_panel_1kg_v1_2tong.manta.chr14.vcf.gz /.../ref_panel_1kg_v1_2tong.manta.chr15.vcf.gz /.../ref_panel_1kg_v1_2tong.manta.chr16.vcf.gz
/.../ref_panel_1kg_v1_2tong.manta.chr17.vcf.gz 
/.../ref_panel_1kg_v1_2tong.manta.chr18.vcf.gz /.../ref_panel_1kg_v1_2tong.manta.chr19.vcf.gz /.../ref_panel_1kg_v1_2tong.manta.chr20.vcf.gz 
/.../ref_panel_1kg_v1_2tong.manta.chr21.vcf.gz /.../ref_panel_1kg_v1_2tong.manta.chr22.vcf.gz 
/.../ref_panel_1kg_v1_2tong.manta.chrX.vcf.gz 
/.../ref_panel_1kg_v1_2tong.manta.chrY.vcf.gz | vcf-sort -c | bgzip -c > ref_panel_1kg_v1_2tong.manta.vcf.gz;
tabix -p vcf ref_panel_1kg_v1_2tong.manta.vcf.gz;
```
#### 生成目录
所在目录：/home/user/zhangtong/gatksv_run/cromwell-executions/Module01/b645dd5f-151c-4284-a7e1-c4768000457e/call-ClusterPESR_manta/ClusterPESR/b1c841db-de67-4318-a198-7e597331539c/call-ConcatVCFs/execution
```
.
| -- docker_cid  
| -- ref_panel_1kg_v1_2tong.manta.vcf.gz      
| -- script             
| -- script.submit  
| -- stderr.background 
| -- stdout.background
| -- rc          
| -- ref_panel_1kg_v1_2tong.manta.vcf.gz.tbi
| -- script.background
| -- stderr         
| -- stdout
```
#### 生成文件
```
ref_panel_1kg_v1_2tong.manta.vcf.gz
ref_panel_1kg_v1_2tong.manta.vcf.gz.tbi
```