### MergeSRFilesByContig
***
#### 作用范围:
for contig in contigs
#### 测试样本:
+ HG00096
+ HG00097
#### 所用docker镜像：
gatksv/sv-base-mini:b3af2e3
#### 所用脚本：
测试:
shard-21:

```xhsell
cd /.../call-MergeSRFilesByContig/shard-21/execution


set -euo pipefail

mkdir data
awk -F "\t" '{if ($1=="chr22") print}' /.../call-MergeSRFilesByContig/
shard-21/inputs/-1454618493/hg38_v0_sv-resources_resources_v1_hg38_primary_contigs.bed > regions.bed
while read file; do
  filename=`basename $file`
  tabix -h -R regions.bed $file > data/$filename.txt
done < /.../call-MergeSRFilesByContig/shard-21/execution/write_lines_e
85380a2f36cb652901ef23c9e2647ee.tmp

mkdir tmp
sort -m -k1,1V -k2,2n -T tmp data/*.txt | bgzip -c > ref_panel_v1.SR.chr22.txt.gz
```
#### 生成文件
shard-21:
```xml
.
├── data
│   ├── SR00c.HG00096.txt.gz.txt
│   └── SR00c.HG00097.txt.gz.txt
├── ref_panel_v1.SR.chr22.txt.gz
├── regions.bed
└── write_lines_e85380a2f36cb652901ef23c9e2647ee.tmp
```