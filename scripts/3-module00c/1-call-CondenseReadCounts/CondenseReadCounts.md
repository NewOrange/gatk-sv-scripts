### CondenseReadCounts
***
#### 前置step:
+ Module00aBatch
#### 作用范围：
for i in range(length(samples))
#### 测试样本:
+ HG00096
+ HG00129
#### 所用docker镜像：
+ ibio01:5000/gatksv/gatk:condensecounts-7396ae99aaab07e29c92b509a6515508fbe68158
#### 所用脚本：
HG00096：
```xhsell
set -e
export GATK_LOCAL_JAR=/root/gatk.jar
gunzip -c /.../HG00096.counts.tsv.gz > counts.tsv
gatk --java-options "-Xmx500m" CondenseReadCounts \
  -I counts.tsv \
  -O condensed_counts.HG00096.tsv \
  --factor 20 \
  --out-bin-length 2000
sed -ri "s/^@RG\tID:GATKCopyNumber\tSM:.+/@RG\tID:GATKCopyNumber\tSM:HG00096/g" condensed_counts.HG00096.tsv
bgzip condensed_counts.HG00096.tsv
```

#### 生成目录
所在目录：/home/user/zhangtong/gatksv_run/cromwell-executions/Module00c/9689f669-dda1-40b4-a6df-aa35c9d84202/call-CondenseReadCounts/shard-0/execution
```xml
.
├── condensed_counts.HG00096.tsv.gz
├── counts.tsv
├── docker_cid
├── rc
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
condensed_counts.HG00096.tsv.gz
```