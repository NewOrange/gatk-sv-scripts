### MergeSRFilesByContig
***
#### 前置step:
+ Module00c.EvidenceMerging.SetSampleIdSR
#### 作用范围：
for contig in contigs
#### 测试样本:
+ HG00096
+ HG00129
#### 所用docker镜像：
+ ibio01:5000/gatksv/sv-base-mini:b3af2e3
#### 所用脚本：
shard-0：
```xhsell
set -euo pipefail

mkdir data
awk -F "\t" '{if ($1=="chr1") print}' /.../hg38_primary_contigs.bed > regions.bed
while read file; do
  filename=`basename $file`
  tabix -h -R regions.bed $file > data/$filename.txt
done < /.../write_lines_c4ecfe4df3ad3932414405e305da125a.tmp

mkdir tmp
sort -m -k1,1V -k2,2n -T tmp data/*.txt | bgzip -c > ref_panel_1kg_v1_2tong.SR.chr1.txt.gz
```

#### 生成目录
所在目录：/home/user/zhangtong/gatksv_run/cromwell-executions/Module00c/c473d627-53ec-45c1-a1c2-e3d4256e0f6c/call-EvidenceMerging/EvidenceMerging/43d86f3a-4d6f-49c4-99c5-95b81cdbe260/call-MergeSRFilesByContig/shard-0/execution
```xml
.
├── data
│   ├── SR00c.HG00096.txt.gz.txt
│   └── SR00c.HG00129.txt.gz.txt
├── docker_cid
├── rc
├── ref_panel_1kg_v1_2tong.SR.chr1.txt.gz
├── regions.bed
├── script
├── script.background
├── script.submit
├── stderr
├── stderr.background
├── stdout
├── stdout.background
├── tmp
└── write_lines_c4ecfe4df3ad3932414405e305da125a.tmp

2 directories, 14 files
```
#### 生成文件
```
ref_panel_1kg_v1_2tong.SR.chr1.txt.gz
```