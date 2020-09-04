### MergePEShards
***
#### 前置step:
+ Module00c.EvidenceMerging.MergePEFilesByContig
#### 作用范围：
for contig in contigs
#### 测试样本:
+ HG00096
+ HG00129
#### 所用docker镜像：
+ ibio01:5000/gatksv/sv-base-mini:b3af2e3
#### 所用脚本：
shard-0：
```xhsell
set -euo pipefail
cat /.../ref_panel_1kg_v1_2tong.PE.chr1.txt.gz /.../ref_panel_1kg_v1_2tong.PE.chr2.txt.gz /.../ref_panel_1kg_v1_2tong.PE.chr3.txt.gz /.../ref_panel_1kg_v1_2tong.PE.chr4.txt.gz /.../ref_panel_1kg_v1_2tong.PE.chr5.txt.gz /.../ref_panel_1kg_v1_2tong.PE.chr6.txt.gz /.../ref_panel_1kg_v1_2tong.PE.chr7.txt.gz /.../ref_panel_1kg_v1_2tong.PE.chr8.txt.gz /.../ref_panel_1kg_v1_2tong.PE.chr9.txt.gz /.../ref_panel_1kg_v1_2tong.PE.chr10.txt.gz /.../ref_panel_1kg_v1_2tong.PE.chr11.txt.gz /.../ref_panel_1kg_v1_2tong.PE.chr12.txt.gz /.../ref_panel_1kg_v1_2tong.PE.chr13.txt.gz /.../ref_panel_1kg_v1_2tong.PE.chr14.txt.gz /.../ref_panel_1kg_v1_2tong.PE.chr15.txt.gz /.../ref_panel_1kg_v1_2tong.PE.chr16.txt.gz /.../ref_panel_1kg_v1_2tong.PE.chr17.txt.gz /.../ref_panel_1kg_v1_2tong.PE.chr18.txt.gz /.../ref_panel_1kg_v1_2tong.PE.chr19.txt.gz /.../ref_panel_1kg_v1_2tong.PE.chr20.txt.gz /.../ref_panel_1kg_v1_2tong.PE.chr21.txt.gz /.../ref_panel_1kg_v1_2tong.PE.chr22.txt.gz /.../ref_panel_1kg_v1_2tong.PE.chrX.txt.gz /.../ref_panel_1kg_v1_2tong.PE.chrY.txt.gz > ref_panel_1kg_v1_2tong.PE.txt.gz
tabix -f -s1 -b2 -e2 ref_panel_1kg_v1_2tong.PE.txt.gz
```

#### 生成目录
所在目录：/home/user/zhangtong/gatksv_run/cromwell-executions/Module00c/c473d627-53ec-45c1-a1c2-e3d4256e0f6c/call-EvidenceMerging/EvidenceMerging/43d86f3a-4d6f-49c4-99c5-95b81cdbe260/call-MergePEShards/execution
```xml
.
├── docker_cid
├── rc
├── ref_panel_1kg_v1_2tong.PE.txt.gz
├── ref_panel_1kg_v1_2tong.PE.txt.gz.tbi
├── script
├── script.background
├── script.submit
├── stderr
├── stderr.background
├── stdout
└── stdout.background

0 directories, 11 files
```
#### 生成文件
```
ref_panel_1kg_v1_2tong.PE.txt.gz
ref_panel_1kg_v1_2tong.PE.txt.gz.tbi
```