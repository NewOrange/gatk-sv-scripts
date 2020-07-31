### MergeSRShards
***
#### 作用范围:
仅一次
#### 测试样本:
+ HG00096
+ HG00097
#### 所用docker镜像：
gatksv/sv-base-mini:b3af2e3
#### 所用脚本：
测试:
```xhsell
cd /.../call-MergePEShards/execution


set -euo pipefail
cat /.../call-MergePEShards/inputs/782595319/ref_panel_v1.PE.chr1.txt.
gz /.../call-MergePEShards/inputs/-1014356040/ref_panel_v1.PE.chr2.txt
.gz /.../call-MergePEShards/inputs/1483659897/ref_panel_v1.PE.chr3.txt
.gz /.../call-MergePEShards/inputs/-313291462/ref_panel_v1.PE.chr4.txt
.gz /.../call-MergePEShards/inputs/-2110242821/ref_panel_v1.PE.chr5.tx
t.gz /.../call-MergePEShards/inputs/387773116/ref_panel_v1.PE.chr6.txt
.gz /.../call-MergePEShards/inputs/-1409178243/ref_panel_v1.PE.chr7.tx
t.gz /.../call-MergePEShards/inputs/1088837694/ref_panel_v1.PE.chr8.tx
t.gz /.../call-MergePEShards/inputs/-708113665/ref_panel_v1.PE.chr9.tx
t.gz /.../call-MergePEShards/inputs/1789902272/ref_panel_v1.PE.chr10.t
xt.gz /.../call-MergePEShards/inputs/-1158940182/ref_panel_v1.PE.chr11
.txt.gz /.../call-MergePEShards/inputs/1339075755/ref_panel_v1.PE.chr1
2.txt.gz /.../call-MergePEShards/inputs/-457875604/ref_panel_v1.PE.chr
13.txt.gz /.../call-MergePEShards/inputs/2040140333/ref_panel_v1.PE.ch
r14.txt.gz /.../call-MergePEShards/inputs/243188974/ref_panel_v1.PE.ch
r15.txt.gz /.../call-MergePEShards/inputs/-1553762385/ref_panel_v1.PE.
chr16.txt.gz /.../call-MergePEShards/inputs/944253552/ref_panel_v1.PE.
chr17.txt.gz /.../call-MergePEShards/inputs/-852697807/ref_panel_v1.PE
.chr18.txt.gz /.../call-MergePEShards/inputs/1645318130/ref_panel_v1.P
E.chr19.txt.gz /.../call-MergePEShards/inputs/-151633229/ref_panel_v1.
PE.chr20.txt.gz /.../call-MergePEShards/inputs/-1029857463/ref_panel_v
1.PE.chr21.txt.gz /.../call-MergePEShards/inputs/1468158474/ref_panel_
v1.PE.chr22.txt.gz /.../call-MergePEShards/inputs/-328792885/ref_panel
_v1.PE.chrX.txt.gz /.../call-MergePEShards/inputs/-2125744244/ref_pane
l_v1.PE.chrY.txt.gz > ref_panel_v1.PE.txt.gz
tabix -f -s1 -b2 -e2 ref_panel_v1.PE.txt.gz
```
#### 生成文件
```xml
.
├── ref_panel_v1.PE.txt.gz
└── ref_panel_v1.PE.txt.gz.tbi
```