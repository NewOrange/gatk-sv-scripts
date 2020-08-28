# Delly_DEL

## 前置step

Step1_CramtoBam

## 所用docker镜像

`gatksv/delly:8645aa`

## 所用脚本

```shell
set -Eeuo pipefail

BCF="HG00096.delly.DEL.bcf"
echo "Running delly on event_type=DEL, output=$BCF"
delly call \
  -t DEL \
  -g "/.../delly_human.hg38.excl.tsv" \
  -o "$BCF" \
  -n \
  "/.../HG00096.final.bam"
```

## 测试目录
所在目录：/home/user/zhangtong/gatksv_run/cromwell-executions/GATKSVPipelineBatch/613a9504-0455-4088-a881-2b793b83ef44/call-Module00aBatch/Module00aBatch/6e2a710b-c9fc-4632-94fa-e2f01eceabbd/call-Module00a/shard-0/Module00a/4ad015d9-2f0e-42c9-bf6f-e9d58604ee3a/call-Delly/Delly/a4388653-2a2f-4473-9f21-79b047bb3baf/call-RunDelly/
```
.
├── docker_cid
├── HG00096.delly.DEL.bcf
├── HG00096.delly.DEL.bcf.csi
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

## 生成文件
```
HG00096.delly.DEL.bcf
HG00096.delly.DEL.bcf.csi
```


