# CollectCounts

## 前置step
Step1_CramtoBam

## 所用docker镜像
`gatksv/gatk:condensecounts-7396ae99aaab07e29c92b509a6515508fbe68158
`

## 测试bam
测试bam：HG00096

## 测试脚本
```shell
set -euo pipefail
export GATK_LOCAL_JAR=/root/gatk.jar

gatk --java-options "-Xmx10240m" CollectReadCounts \
  -L /.../preprocessed_intervals.inte
rval_list \
  --input /.../HG00096.final.bam \
  --reference /.../Homo_sapiens_assembly38.fasta \
  --format TSV \
  --interval-merging-rule OVERLAPPING_ONLY \
  --output HG00096.counts.tsv \
  --disable-read-filter MappingQualityReadFilter

sed -ri "s/@RG\tID:GATKCopyNumber\tSM:.+/@RG\tID:GATKCopyNumber\tSM:HG00096/g" HG00096.counts.tsv
bgzip HG00096.counts.tsv
```
## 测试目录
所在目录：/home/user/zhangtong/gatksv_run/cromwell-executions/GATKSVPipelineBatch/613a9504-0455-4088-a881-2b793b83ef44/call-Module00aBatch/Module00aBatch/6e2a710b-c9fc-4632-94fa-e2f01eceabbd/call-Module00a/shard-0/Module00a/4ad015d9-2f0e-42c9-bf6f-e9d58604ee3a/call-CollectCounts/execution
```xml
.
├── docker_cid
├── HG00096.counts.tsv.gz
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
HG00096.counts.tsv.gz
```