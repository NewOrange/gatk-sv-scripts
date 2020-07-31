### SetSampleIdSR
***
#### 作用范围:
for i in range(length(samples))
#### 测试样本:
+ HG00096
+ HG00097
#### 所用docker镜像：
gatksv/sv-base-mini:b3af2e3
#### 所用脚本：
测试:
shard-0:
```xhsell
cd /.../call-SetSampleIdSR/shard-0/execution


set -euo pipefail
zcat /.../call-SetSampleIdSR/shard-0/inputs/1502637670/HG00096.chr22.s
plit.txt.gz | awk -F "\t" -v OFS="\t" '$5="HG00096"' | bgzip -c > SR00c.HG00096.txt.gz
tabix -s1 -b2 -e2 SR00c.HG00096.txt.gz
```
#### 生成文件
shard-0:
```xml
.
├── SR00c.HG00096.txt.gz
├── SR00c.HG00096.txt.gz.tbi
└── SR00c.HG00096.txt.gz.tbi
```