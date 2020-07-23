### CondenseReadCounts
***
#### 前置step:
Module00a.step2
#### 测试样本:
+ HG00096
+ HG00097
#### 所用docker镜像：
Todo
#### 所用脚本：
测试：
shard-0：
```xhsell
cd /.../shard-0/execution


set -e
export GATK_LOCAL_JAR=/root/gatk.jar
gunzip -c /cromwell-executions/GATKSVPipelinePhase1/8d210b54-725e-47f8-aa63-3c21b9aa8f31/call-Module00c/Module00c/b362d99d-0e0b-47
a8-8322-c6bd753e915f/call-CondenseReadCounts/shard-0/inputs/1502637668/HG00096.chr22.counts.tsv.gz > counts.tsv
gatk --java-options "-Xmx500m" CondenseReadCounts \
  -I counts.tsv \
  -O condensed_counts.HG00096.tsv \
  --factor 20 \
  --out-bin-length 2000
sed -ri "s/^@RG\tID:GATKCopyNumber\tSM:.+/@RG\tID:GATKCopyNumber\tSM:HG00096/g" condensed_counts.HG00096.tsv
bgzip condensed_counts.HG00096.tsv
```
shard-1：
```shell
cd /.../shard-1/execution


set -e
export GATK_LOCAL_JAR=/root/gatk.jar
gunzip -c /cromwell-executions/GATKSVPipelinePhase1/8d210b54-725e-47f8-aa63-3c21b9aa8f31/call-Module00c/Module00c/b362d99d-0e0b-47
a8-8322-c6bd753e915f/call-CondenseReadCounts/shard-1/inputs/1502637668/HG00097.chr22.counts.tsv.gz > counts.tsv
gatk --java-options "-Xmx500m" CondenseReadCounts \
  -I counts.tsv \
  -O condensed_counts.HG00097.tsv \
  --factor 20 \
  --out-bin-length 2000
sed -ri "s/^@RG\tID:GATKCopyNumber\tSM:.+/@RG\tID:GATKCopyNumber\tSM:HG00097/g" condensed_counts.HG00097.tsv
bgzip condensed_counts.HG00097.tsv
```
#### inputs
```xml
shard-0: HG00096.chr22.counts.tsv.gz
shard-1: HG00097.chr22.counts.tsv.gz
```

#### 生成结果
```xml
.
├── shard-0
│   ├── condensed_counts.HG00096.tsv.gz
│   ├── counts.tsv
│   └── rc
├── shard-1
│   ├── condensed_counts.HG00097.tsv.gz
│   ├── counts.tsv
│   └── rc
```