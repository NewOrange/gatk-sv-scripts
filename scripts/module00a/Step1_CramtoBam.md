# CramToBam

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
    -@ 2 \
    -T /mnt/d/Works/genes/0629/gatk/data/gcp-public-data--broad-references/hg38/v0/Homo_sapiens_assembly38.fasta \
    -o /mnt/d/Works/genes/0629/gatk/data/fc-56ac46ea-efc4-4683-b6d5-6d95bed41c5e/CCDG_13607/Project_CCDG_13607_B01_GRM_WGS.cram.2019-02-06/Sample_HG00096/analysis/HG00096.final.bam \
    /mnt/d/Works/genes/0629/gatk/data/fc-56ac46ea-efc4-4683-b6d5-6d95bed41c5e/CCDG_13607/Project_CCDG_13607_B01_GRM_WGS.cram.2019-02-06/Sample_HG00096/analysis/HG00096.final.cram

# index bam file
samtools index -@ 2 /mnt/d/Works/genes/0629/gatk/data/fc-56ac46ea-efc4-4683-b6d5-6d95bed41c5e/CCDG_13607/Project_CCDG_13607_B01_GRM_WGS.cram.2019-02-06/Sample_HG00096/analysis/HG00096.final.bam
```

## 测试结果

```txt
$ ls -lh /mnt/d/Works/genes/0629/gatk/data/fc-56ac46ea-efc4-4683-b6d5-6d95bed41c5e/CCDG_13607/Project_CCDG_13607_B01_GRM_WGS.cram.2019-02-06/Sample_HG00096/analysis/
total 55G
-rwxrwxrwx 1 sdiodio sdiodio  40G Jul 20 15:21 HG00096.final.bam
-rwxrwxrwx 1 sdiodio sdiodio 8.9M Jul 20 16:01 HG00096.final.bam.bai
-rwxrwxrwx 1 sdiodio sdiodio  15G Jun 30 15:18 HG00096.final.cram
-rwxrwxrwx 1 sdiodio sdiodio 1.4M Jul  1 15:11 HG00096.final.cram.crai
drwxrwxrwx 1 sdiodio sdiodio 4.0K Jul  1 15:12 checksum
$
$ tree /mnt/d/Works/genes/0629/gatk/data/fc-56ac46ea-efc4-4683-b6d5-6d95bed41c5e/CCDG_13607/Project_CCDG_
13607_B01_GRM_WGS.cram.2019-02-06/Sample_HG00096/analysis/
/mnt/d/Works/genes/0629/gatk/data/fc-56ac46ea-efc4-4683-b6d5-6d95bed41c5e/CCDG_13607/Project_CCDG_13607_B01_GRM_WGS.cram.2019-02-06/Sample_HG00096/analysis/
├── HG00096.final.bam
├── HG00096.final.bam.bai
├── HG00096.final.cram
├── HG00096.final.cram.crai
└── checksum
    ├── HG00096.final.cram.crai.md5
    └── HG00096.final.cram.md5

1 directory, 6 files
```
