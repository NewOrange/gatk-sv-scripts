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
vcf-concat /.../ref_panel_v1.manta.chr1.vcf.gz /.../ref_panel_v1.manta.chr2.vcf.gz 
/.../ref_panel_v1.manta.chr3.vcf.gz 
/.../ref_panel_v1.manta.chr4.vcf.gz 
/.../ref_panel_v1.manta.chr5.vcf.gz 
/.../ref_panel_v1.manta.chr6.vcf.gz 
/.../ref_panel_v1.manta.chr7.vcf.gz 
/.../ref_panel_v1.manta.chr8.vcf.gz 
/.../ref_panel_v1.manta.chr9.vcf.gz
/.../ref_panel_v1.manta.chr10.vcf.gz /.../ref_panel_v1.manta.chr11.vcf.gz /.../ref_panel_v1.manta.chr12.vcf.gz /.../ref_panel_v1.manta.chr13.vcf.gz 
/.../ref_panel_v1.manta.chr14.vcf.gz /.../ref_panel_v1.manta.chr15.vcf.gz /.../ref_panel_v1.manta.chr16.vcf.gz
/.../ref_panel_v1.manta.chr17.vcf.gz 
/.../ref_panel_v1.manta.chr18.vcf.gz /.../ref_panel_v1.manta.chr19.vcf.gz /.../ref_panel_v1.manta.chr20.vcf.gz 
/.../ref_panel_v1.manta.chr21.vcf.gz /.../ref_panel_v1.manta.chr22.vcf.gz 
/.../ref_panel_v1.manta.chrX.vcf.gz 
/.../ref_panel_v1.manta.chrY.vcf.gz | vcf-sort -c | bgzip -c > ref_panel_v1.manta.vcf.gz;
tabix -p vcf ref_panel_v1.manta.vcf.gz;
```
#### 生成目录
```
.
├── ref_panel_v1.manta.vcf.gz.tbi
└── ref_panel_v1.manta.vcf.gz.tbi
```