### SetSampleIdSR
***
#### 前置step:
+ Module00aBatch
#### 作用范围：
for i in range(length(samples)
#### 测试样本:
+ HG00096
+ HG00129
#### 所用docker镜像：
+ ibio01:5000/gatksv/sv-base-mini:b3af2e3
#### 所用脚本：
HG00096：
```xhsell
set -euo pipefail
zcat /.../HG00096.split.txt.gz | awk -F "\t" -v OFS="\t" '$5="HG00096"' | bgzip -c > SR00c.HG00096.txt.gz
tabix -s1 -b2 -e2 SR00c.HG00096.txt.gz
```

#### 生成目录
所在目录：/home/user/zhangtong/gatksv_run/cromwell-executions/Module00c/c473d627-53ec-45c1-a1c2-e3d4256e0f6c/call-EvidenceMerging/EvidenceMerging/43d86f3a-4d6f-49c4-99c5-95b81cdbe260/call-SetSampleIdSR/shard-0/execution
```xml
.
├── docker_cid
├── rc
├── script
├── script.background
├── script.submit
├── SR00c.HG00096.txt.gz
├── SR00c.HG00096.txt.gz.tbi
├── stderr
├── stderr.background
├── stdout
└── stdout.background

0 directories, 11 files
```
#### 生成文件
```
SR00c.HG00096.txt.gz
SR00c.HG00096.txt.gz.tbi
```