#### CramToBam
***
#### 前置step:
无

#### 所用docker镜像：
gatksv/samtools-cloud:b3af2e3

Tips: This version localizes the cram since samtools does not support streaming from requester pays buckets

#### 所用脚本：
测试：
```shell
        set -Eeuo pipefail

        # covert cram to bam
        samtools view \
                 -b \
                 -h \
                 -@ 2 \
                 -T /mnt/d/Works/genes/0629/gatk/data/gcp-public-data--broad-references/hg38/v0/Homo_sapiens_assembly38.fasta \
                 -o /mnt/d/Works/genes/0629/gatk/data/fc-56ac46ea-efc4-4683-b6d5-6d95bed41c5e/CCDG_13607/Project_CCDG_13607_B01_GRM_WGS.cram.2019-02-06/Sample_HG00096/analysis/HG00096.final.bam \
                 /mnt/d/Works/genes/0629/gatk/data/fc-56ac46ea-efc4-4683-b6d5-6d95bed41c5e/CCDG_13607/Project_CCDG_13607_B01_GRM_WGS.cram.2019-02-06/Sample_HG00096/analysis/HG00096.final.cram

        # index bam file
        samtools index -@ 2 /mnt/d/Works/genes/0629/gatk/data/fc-56ac46ea-efc4-4683-b6d5-6d95bed41c5e/CCDG_13607/Project_CCDG_13607_B01_GRM_WGS.cram.2019-02-06/Sample_HG00096/analysis/HG00096.final.bam
```
