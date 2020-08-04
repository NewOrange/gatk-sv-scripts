### ConcatVCFs
***
#### 前置step:
VCFCluster
#### 测试样本:
+ HG00096
+ HG00097
#### 所用docker镜像：
gatksv/sv-base-mini:b3af2e3
#### 所用脚本：
测试：
```xhsell
cd /.../call-ConcatVCFs/execution


set -euo pipefail
vcf-concat /.../ref_panel_v1.delly.chr1.vcf.gz /.../ref_panel_v1.delly.chr2.vcf.gz 
/.../ref_panel_v1.delly.chr3.vcf.gz 
/.../ref_panel_v1.delly.chr4.vcf.gz 
/.../ref_panel_v1.delly.chr5.vcf.gz 
/.../ref_panel_v1.delly.chr6.vcf.gz 
/.../ref_panel_v1.delly.chr7.vcf.gz 
/.../ref_panel_v1.delly.chr8.vcf.gz 
/.../ref_panel_v1.delly.chr9.vcf.gz
/.../ref_panel_v1.delly.chr10.vcf.gz /.../ref_panel_v1.delly.chr11.vcf.gz /.../ref_panel_v1.delly.chr12.vcf.gz /.../ref_panel_v1.delly.chr13.vcf.gz 
/.../ref_panel_v1.delly.chr14.vcf.gz /.../ref_panel_v1.delly.chr15.vcf.gz /.../ref_panel_v1.delly.chr16.vcf.gz
/.../ref_panel_v1.delly.chr17.vcf.gz 
/.../ref_panel_v1.delly.chr18.vcf.gz /.../ref_panel_v1.delly.chr19.vcf.gz /.../ref_panel_v1.delly.chr20.vcf.gz 
/.../ref_panel_v1.delly.chr21.vcf.gz /.../ref_panel_v1.delly.chr22.vcf.gz 
/.../ref_panel_v1.delly.chrX.vcf.gz 
/.../ref_panel_v1.delly.chrY.vcf.gz | vcf-sort -c | bgzip -c > ref_panel_v1.delly.vcf.gz;
tabix -p vcf ref_panel_v1.delly.vcf.gz;
```
#### 生成目录
```
.
├── ref_panel_v1.delly.vcf.gz.tbi
└── ref_panel_v1.delly.vcf.gz.tbi
```