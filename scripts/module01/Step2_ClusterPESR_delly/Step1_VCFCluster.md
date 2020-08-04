### VCFCluster
***
#### 前置step:
Module00c.PreprocessPESR
#### 作用范围：
for contig in contiglist
#### 测试样本:
+ HG00096
+ HG00097
#### 所用docker镜像：
cwhelan/sv-pipeline:cw_3c9d26c_single_sample_annotations
#### 所用脚本：
测试：
shard-21
```xhsell

cd /.../call-VCFCluster/shard-21/execution


set -euo pipefail
for f in /.../call-VCFCluster/shard-21/inputs/-2117685912/std_000.delly.HG00096.vcf.gz /.../call-VCFCluster/shard-21/inputs/-2117685912/std_001.delly.HG00097.vcf.gz; do tabix -p vcf -f
$f; done;
tabix -p bed /.../call-VCFCluster/shard-21/inputs/-1454618493/hg38_v0_sv-resources_resources_v1_PESR.encode.peri_all.repeats.delly.hg38.blacklist.bed.gz;

svtk vcfcluster /.../call-VCFCluster/shard-21/execution/write_lines_7833ee058aee84a4a4695d68b2ab7dcb.tmp stdout \
  -r chr22 \
  -p ref_panel_v1_delly_chr22 \
  -d 300 \
  -f 0.1 \
  -x /.../call-VCFCluster/shard-21/inputs/-1454618493/hg38_v0_sv-resources_resources_v1_PESR.encode.peri_all.repeats.delly.hg38.blacklist.bed.gz \
  -z 0 \
  -t DEL,DUP,INV,BND,INS \
  --preserve-ids \
  | vcf-sort -c \
  | bgzip -c > ref_panel_v1.delly.chr22.vcf.gz
```
#### 生成目录
```
.
├── ref_panel_v1.delly.chr22.vcf.gz
└── write_lines_7833ee058aee84a4a4695d68b2ab7dcb.tmp
```