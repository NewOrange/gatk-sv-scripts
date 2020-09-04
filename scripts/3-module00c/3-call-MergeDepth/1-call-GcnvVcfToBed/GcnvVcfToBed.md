### GcnvVcfToBed
***
#### 前置step:
+ Module00c.gCNVCase
+ Module00c.CNMOPS
+ Module00c.CNMOPSLarge
#### 作用范围：
for i in range(length(samples))
#### 测试样本:
+ HG00096
+ HG00129
#### 所用docker镜像：
+ ibio01:5000/cwhelan/sv-pipeline:cw_3c9d26c_single_sample_annotations
#### 所用脚本：
HG00096：
```xhsell
set -e
tar xzf /.../sample_000.HG00096.contig_ploidy_calls.tar.gz
tabix /.../genotyped-segments-HG00096.vcf.gz
python /opt/WGD/bin/convert_gcnv.py \
  --cutoff 30 \
  contig_ploidy.tsv \
  /.../genotyped-segments-HG00096.vcf.gz \
  HG00096
```

#### 生成目录
所在目录：/home/user/zhangtong/gatksv_run/cromwell-executions/Module00c/9689f669-dda1-40b4-a6df-aa35c9d84202/call-MergeDepth/MergeDepth/86744103-1c75-47aa-be83-cdcba8448706/call-GcnvVcfToBed/shard-0/execution
```xml
.
├── contig_ploidy.tsv
├── docker_cid
├── global_read_depth.tsv
├── HG00096.del.bed
├── HG00096.dup.bed
├── mu_psi_s_log__.tsv
├── rc
├── sample_name.txt
├── script
├── script.background
├── script.submit
├── stderr
├── stderr.background
├── stdout
├── stdout.background
└── std_psi_s_log__.tsv

0 directories, 16 files
```
#### 生成文件
```
HG00096.del.bed
HG00096.dup.bedmore 
```