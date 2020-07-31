### SetSampleIdPE
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
cd /.../call-SetSampleIdPE/shard-0/execution


set -euo pipefail
zcat /.../call-SetSampleIdPE/shard-0/inputs/1502637670/HG00096.chr22.d
isc.txt.gz | awk -F "\t" -v OFS="\t" '$7="HG00096"' | bgzip -c > PE00c.HG00096.txt.gz
tabix -s1 -b2 -e2 PE00c.HG00096.txt.gz
```
#### 生成文件
shard-0:
```xml
.
├── PE00c.HG00096.txt.gz
└── PE00c.HG00096.txt.gz.tbi
```