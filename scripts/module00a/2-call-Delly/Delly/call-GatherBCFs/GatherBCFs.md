# GatherBCFs

## 前置step

RunDelly

## 所用docker镜像

`gatksv/delly:8645aa`

## 所用脚本

```shell

    set -Eeuo pipefail

    BCFS="/.../HG00096.delly.DEL.bcf
/.../HG00096.delly.DUP.bcf
/.../HG00096.delly.INV.bcf"
    echo "Extracting vcf header"
    bcftools view /.../HG00096.delly.DEL.bcf | grep "^#" > header.vcf
    VCFS="header.vcf"
    for ((BCF_IND=1; BCF_IND <= 3; BCF_IND++)); do
      echo "Processing BCF $BCF_IND"
      BCF=$(echo "$BCFS" | sed "$BCF_IND""q;d")
      VCF=$(echo "$BCF" | sed -e 's/.bcf$/.vcf/')
      echo "Converting $BCF to $VCF, skipping header"
      bcftools view  $BCF | grep -v "^#" > $VCF
      VCFS="$VCFS $VCF"
    done

    VCF_OUT="HG00096.delly.vcf.gz"
    echo "Concatenating vcfs into $VCF_OUT"
    cat $VCFS \
      | vcf-sort -c \
      | bcftools reheader -s <(echo "HG00096") \
      | bgzip -c \
      > $VCF_OUT
    echo "Indexing $VCF_OUT"
    tabix "$VCF_OUT"
```

## 测试目录
所在目录：/home/user/zhangtong/gatksv_run/cromwell-executions/GATKSVPipelineBatch/613a9504-0455-4088-a881-2b793b83ef44/call-Module00aBatch/Module00aBatch/6e2a710b-c9fc-4632-94fa-e2f01eceabbd/call-Module00a/shard-0/Module00a/4ad015d9-2f0e-42c9-bf6f-e9d58604ee3a/call-Delly/Delly/a4388653-2a2f-4473-9f21-79b047bb3baf/call-GatherBCFs/execution
```
.
├── docker_cid
├── header.vcf
├── HG00096.delly.vcf.gz
├── HG00096.delly.vcf.gz.tbi
├── rc
├── script
├── script.background
├── script.submit
├── stderr
├── stderr.background
├── stdout
└── stdout.background

0 directories, 12 files
```

## 生成文件
```
HG00096.delly.vcf.gz
HG00096.delly.vcf.gz.tbi
```


