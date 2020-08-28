# RunPESRCollection

## 前置step
Step1_CramtoBam

## 所用docker镜像
`cwhelan/sv-pipeline:cw_3c9d26c_single_sample_annotations
`
## 测试bam
测试bam：HG00096

## 测试脚本
```shell
set -euo pipefail

export GATK_LOCAL_JAR=/root/gatk.jar

/gatk/gatk --java-options "-Xmx3250m" PairedEndAndSplitReadEvidenceCollection \
    -I /.../HG00096.final.bam \
    --pe-file HG00096.disc.txt.gz \
    --sr-file HG00096.split.txt.gz \
    --sample-name HG00096 \
    -R /.../Homo_sapiens_assembly38.fasta

tabix -f -s1 -b 2 -e 2 HG00096.disc.txt.gz
tabix -f -s1 -b 2 -e 2 HG00096.split.txt.gz
```
## 测试目录
所在目录：/home/user/zhangtong/gatksv_run/cromwell-executions/GATKSVPipelineBatch/613a9504-0455-4088-a881-2b793b83ef44/call-Module00aBatch/Module00aBatch/6e2a710b-c9fc-4632-94fa-e2f01eceabbd/call-Module00a/shard-0/Module00a/4ad015d9-2f0e-42c9-bf6f-e9d58604ee3a/call-PESRCollection/PESRCollection/3afc09f7-e645-498a-af6c-aae00f192aa5/call-RunPESRCollection/execution
```xml
.
├── docker_cid
├── HG00096.disc.txt.gz
├── HG00096.disc.txt.gz.tbi
├── HG00096.split.txt.gz
├── HG00096.split.txt.gz.tbi
├── rc
├── script
├── script.background
├── script.submit
├── stderr
├── stderr.background
├── stdout
└── stdout.background

0 directories, 13 files
```
## 生成文件
```
HG00096.disc.txt.gz
HG00096.disc.txt.gz.tbi
HG00096.split.txt.gz
HG00096.split.txt.gz.tbi
```