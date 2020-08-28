# RunCramToBamRequesterPays

## 前置step

无

## 所用docker镜像

gatksv/samtools-cloud:b3af2e3

Tips: This version localizes the cram since samtools does not support streaming from requester pays buckets

## 所用脚本

测试：

```shell
set -Eeuo pipefail

# covert cram to bam
samtools view \
         -b \
         -h \
         -@ 4 \
         -T "/.../Homo_sapiens_assembly38.fasta" \
         -o "HG00096.final.bam" \
         "/.../HG00096.final.cram"

# index bam file
samtools index -@ 4 "HG00096.final.bam"
```
## 测试目录
所在目录：/home/user/zhangtong/gatksv_run/cromwell-executions/GATKSVPipelineBatch/30b24ee2-fd82-4c55-80a2-6f78ba2e9ab6/call-Module00aBatch/Module00aBatch/33531071-8db5-4864-a123-3bad6950a142/call-Module00a/shard-0/Module00a/71546613-ccf7-48a9-8419-d7f71fc2e6ec/call-CramToBam/CramToBam/6f1aded2-7135-463e-83b9-028a3d263f30/call-RunCramToBamRequesterPays/execution
```
.
├── HG00096.final.bam
├── HG00096.final.bam.bai
├── rc
├── script
├── script.background
├── script.submit
├── stderr
├── stderr.background
├── stdout
└── stdout.background

0 directories, 10 files
```
## 生成文件
```
HG00096.final.bam
HG00096.final.bam.bai
```
