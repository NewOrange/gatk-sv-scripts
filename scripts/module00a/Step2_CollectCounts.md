# CollectCounts(Optional)

collect_coverage参数为true

## 前置step

Step1_CramtoBam

#### 所用docker镜像

gatksv/gatk:condensecounts-7396ae99aaab07e29c92b509a6515508fbe68158

#### 所用脚本

原版：

```shell
set -euo pipefail
export GATK_LOCAL_JAR=~{default="/root/gatk.jar" gatk4_jar_override}

gatk --java-options "-Xmx~{command_mem_mb}m" CollectReadCounts \
	-L ~{intervals} \
	--input ~{bam} \
	--reference ~{ref_fasta} \
	--format TSV \
	--interval-merging-rule OVERLAPPING_ONLY \
	--output ~{sample_id}.counts.tsv \
	~{sep=' ' disabled_read_filters_arr}

sed -ri "s/@RG\tID:GATKCopyNumber\tSM:.+/@RG\tID:GATKCopyNumber\tSM:~{sample_id}/g" ~{sample_id}.counts.tsv

bgzip ~{sample_id}.counts.tsv
```

测试：

```shell
set -euo pipefail
export GATK_LOCAL_JAR="/root/gatk.jar"

gatk --java-options "-Xmx3500m" CollectReadCounts \
	-L /mnt/d/Works/genes/0629/gatk/data/gatk-sv-resources-public/hg38/v0/sv-resources/resources/v1/preprocessed_intervals.interval_list \
	--input /mnt/d/Works/genes/0629/gatk/data/fc-56ac46ea-efc4-4683-b6d5-6d95bed41c5e/CCDG_13607/Project_CCDG_13607_B01_GRM_WGS.cram.2019-02-06/Sample_HG00096/analysis/HG00096.final.bam \
	--reference /mnt/d/Works/genes/0629/gatk/data/gcp-public-data--broad-references/hg38/v0/Homo_sapiens_assembly38.fasta \
	--format TSV \
	--interval-merging-rule OVERLAPPING_ONLY \
	--output HG00096.counts.tsv \
	--disable-read-filter MappingQualityReadFilter

sed -ri "s/@RG\tID:GATKCopyNumber\tSM:.+/@RG\tID:GATKCopyNumber\tSM:~HG00096/g" HG00096.counts.tsv

bgzip HG00096.counts.tsv
```
