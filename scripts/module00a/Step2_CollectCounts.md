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

gatk --java-options "-Xmx14000m" CollectReadCounts \
	-L /test_data/sv-resources/resources/v1/hg38_v0_sv-resources_resources_v1_preprocessed_intervals.interval_list \
	--input /test_data/bam/HG00096.chr22.bam \
	--reference /test_data/ref_data/hg38_v0_Homo_sapiens_assembly38.fasta \
	--format TSV \
	--interval-merging-rule OVERLAPPING_ONLY \
	--output HG00096.chr22.counts.tsv \
	--disable-read-filter MappingQualityReadFilter

sed -ri "s/@RG\tID:GATKCopyNumber\tSM:.+/@RG\tID:GATKCopyNumber\tSM:~HG00096/g" HG00096.chr22.counts.tsv

bgzip HG00096.chr22.counts.tsv
```

#### 测试日志：
```shell
04:36:06.023 WARN  GATKReadFilterPluginDescriptor - Values were supplied for (MappingQualityReadFilter) that is also disabled
04:36:06.072 INFO  NativeLibraryLoader - Loading libgkl_compression.so from jar:file:/gatk/gatk-package-4.0.12.0-97-g7396ae9-SNAPSHOT-local.jar!/com/intel/gkl/native/libgkl_compression.so
04:36:07.861 INFO  CollectReadCounts - ------------------------------------------------------------
04:36:07.862 INFO  CollectReadCounts - The Genome Analysis Toolkit (GATK) v4.0.12.0-97-g7396ae9-SNAPSHOT
04:36:07.862 INFO  CollectReadCounts - For support and documentation go to https://software.broadinstitute.org/gatk/
04:36:07.863 INFO  CollectReadCounts - Executing as root@0ea6ac780a90 on Linux v4.15.0-96-generic amd64
04:36:07.863 INFO  CollectReadCounts - Java runtime: OpenJDK 64-Bit Server VM v1.8.0_191-8u191-b12-0ubuntu0.16.04.1-b12
04:36:07.863 INFO  CollectReadCounts - Start Date/Time: July 22, 2020 4:36:06 AM UTC
04:36:07.863 INFO  CollectReadCounts - ------------------------------------------------------------
04:36:07.863 INFO  CollectReadCounts - ------------------------------------------------------------
04:36:07.864 INFO  CollectReadCounts - HTSJDK Version: 2.18.2
04:36:07.864 INFO  CollectReadCounts - Picard Version: 2.18.25
04:36:07.864 INFO  CollectReadCounts - HTSJDK Defaults.COMPRESSION_LEVEL : 2
04:36:07.865 INFO  CollectReadCounts - HTSJDK Defaults.USE_ASYNC_IO_READ_FOR_SAMTOOLS : false
04:36:07.865 INFO  CollectReadCounts - HTSJDK Defaults.USE_ASYNC_IO_WRITE_FOR_SAMTOOLS : true
04:36:07.865 INFO  CollectReadCounts - HTSJDK Defaults.USE_ASYNC_IO_WRITE_FOR_TRIBBLE : false
04:36:07.865 INFO  CollectReadCounts - Deflater: IntelDeflater
04:36:07.865 INFO  CollectReadCounts - Inflater: IntelInflater
04:36:07.865 INFO  CollectReadCounts - GCS max retries/reopens: 20
04:36:07.865 INFO  CollectReadCounts - Requester pays: disabled
04:36:07.865 INFO  CollectReadCounts - Initializing engine
WARNING: BAM index file /test_data/bam/HG00096.part.bam.bai is older than BAM /test_data/bam/HG00096.part.bam
04:37:28.920 INFO  IntervalArgumentCollection - Processing 2923733770 bp from intervals
04:37:51.477 INFO  CollectReadCounts - Done initializing engine
04:37:51.481 INFO  CollectReadCounts - Initializing and validating intervals...
04:39:00.518 INFO  CollectReadCounts - Collecting read counts...
04:39:00.518 INFO  ProgressMeter - Starting traversal
04:39:00.519 INFO  ProgressMeter -        Current Locus  Elapsed Minutes       Reads Processed     Reads/Minute
04:39:10.554 INFO  ProgressMeter -       chr22:15417117              0.2                734000        4395648.3
04:39:20.593 INFO  ProgressMeter -       chr22:21402255              0.3               2295000        6859961.1
04:39:30.594 INFO  ProgressMeter -       chr22:29187046              0.5               4166000        8311221.9
04:39:40.596 INFO  ProgressMeter -       chr22:38371430              0.7               6412000        9599520.9
04:39:50.597 INFO  ProgressMeter -       chr22:47269338              0.8               8657000       10372219.3
04:39:54.772 INFO  CollectReadCounts - 1021808 read(s) filtered by: (((WellformedReadFilter AND MappedReadFilter) AND NonZeroReferenceLengthAlignmentReadFilter) AND NotDuplicateReadFilter)
  14653 read(s) filtered by: ((WellformedReadFilter AND MappedReadFilter) AND NonZeroReferenceLengthAlignmentReadFilter)
      14653 read(s) filtered by: (WellformedReadFilter AND MappedReadFilter)
          14653 read(s) filtered by: MappedReadFilter
  1007155 read(s) filtered by: NotDuplicateReadFilter

04:39:54.772 INFO  ProgressMeter -       chr22:50808012              0.9               9554944       10567095.6
04:39:54.772 INFO  ProgressMeter - Traversal complete. Processed 9554944 total reads in 0.9 minutes.
04:39:54.772 INFO  CollectReadCounts - Writing read counts to HG00096.counts.tsv
04:41:39.932 INFO  CollectReadCounts - Shutting down engine
[July 22, 2020 4:41:39 AM UTC] org.broadinstitute.hellbender.tools.copynumber.CollectReadCounts done. Elapsed time: 5.56 minutes.
Runtime.totalMemory()=12030312448
Tool returned:
SUCCESS
```
#### 生成文件：
```
step02
└── HG00096.chr22.counts.tsv.gz

0 directories, 1 file
```