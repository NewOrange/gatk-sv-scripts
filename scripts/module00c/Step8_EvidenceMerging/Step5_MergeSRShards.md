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
cd /.../call-MergeSRShards/execution


set -euo pipefail
cat /.../call-MergeSRShards/inputs/-1835014323/ref_panel_v1.SR.chr1.tx
t.gz /.../call-MergeSRShards/inputs/663001614/ref_panel_v1.SR.chr2.txt
.gz /.../call-MergeSRShards/inputs/-1133949745/ref_panel_v1.SR.chr3.tx
t.gz /.../call-MergeSRShards/inputs/1364066192/ref_panel_v1.SR.chr4.tx
t.gz /.../call-MergeSRShards/inputs/-432885167/ref_panel_v1.SR.chr5.tx
t.gz /.../call-MergeSRShards/inputs/2065130770/ref_panel_v1.SR.chr6.tx
t.gz /.../call-MergeSRShards/inputs/268179411/ref_panel_v1.SR.chr7.txt
.gz /.../call-MergeSRShards/inputs/-1528771948/ref_panel_v1.SR.chr8.tx
t.gz /.../call-MergeSRShards/inputs/969243989/ref_panel_v1.SR.chr9.txt
.gz /.../call-MergeSRShards/inputs/-827707370/ref_panel_v1.SR.chr10.tx
t.gz /.../call-MergeSRShards/inputs/-700460460/ref_panel_v1.SR.chr11.t
xt.gz /.../call-MergeSRShards/inputs/1797555477/ref_panel_v1.SR.chr12.
txt.gz /.../call-MergeSRShards/inputs/604118/ref_panel_v1.SR.chr13.txt
.gz /.../call-MergeSRShards/inputs/-1796347241/ref_panel_v1.SR.chr14.t
xt.gz /.../call-MergeSRShards/inputs/701668696/ref_panel_v1.SR.chr15.t
xt.gz /.../call-MergeSRShards/inputs/-1095282663/ref_panel_v1.SR.chr16
.txt.gz /.../call-MergeSRShards/inputs/1402733274/ref_panel_v1.SR.chr1
7.txt.gz /.../call-MergeSRShards/inputs/-394218085/ref_panel_v1.SR.chr
18.txt.gz /.../call-MergeSRShards/inputs/2103797852/ref_panel_v1.SR.ch
r19.txt.gz /.../call-MergeSRShards/inputs/306846493/ref_panel_v1.SR.ch
r20.txt.gz /.../call-MergeSRShards/inputs/-571377741/ref_panel_v1.SR.c
hr21.txt.gz /.../call-MergeSRShards/inputs/1926638196/ref_panel_v1.SR.
chr22.txt.gz /.../call-MergeSRShards/inputs/129686837/ref_panel_v1.SR.
chrX.txt.gz /.../call-MergeSRShards/inputs/-1667264522/ref_panel_v1.SR
.chrY.txt.gz > ref_panel_v1.SR.txt.gz
tabix -f -s1 -b2 -e2 ref_panel_v1.SR.txt.gz
```
#### 生成文件
```xml
.
├── ref_panel_v1.SR.txt.gz
└── ref_panel_v1.SR.txt.gz.tbi
```