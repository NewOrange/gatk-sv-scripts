# GatherBCFs

## 前置step

Step5_Delly

## 所用docker镜像

`gatksv/sv-base-mini:b3af2e3`

## 所用脚本

原版：
```shell
    set -Eeuo pipefail

    BCFS="~{sep='\n' bcfs}"
    echo "Extracting vcf header"
    bcftools view ~{first_bcf} | grep "^#" > header.vcf
    VCFS="header.vcf"
    for ((BCF_IND=1; BCF_IND <= ~{num_bcfs}; BCF_IND++)); do
      echo "Processing BCF $BCF_IND"
      BCF=$(echo "$BCFS" | sed "$BCF_IND""q;d")
      VCF=$(echo "$BCF" | sed -e 's/.bcf$/.vcf/')
      echo "Converting $BCF to $VCF, skipping header"
      bcftools view  $BCF | grep -v "^#" > $VCF
      VCFS="$VCFS $VCF"
    done

    VCF_OUT="~{sample_id}.delly.vcf.gz"
    echo "Concatenating vcfs into $VCF_OUT"
    cat $VCFS \
      | vcf-sort -c \
      | bcftools reheader -s <(echo "~{sample_id}") \
      | bgzip -c \
      > $VCF_OUT
    echo "Indexing $VCF_OUT"
    tabix "$VCF_OUT"
```

## 测试：
### 生成文件：

```xml
step06
├── HG00096.delly.vcf.gz
└── HG00096.delly.vcf.gz.tbi

0 directories, 2 files
```
