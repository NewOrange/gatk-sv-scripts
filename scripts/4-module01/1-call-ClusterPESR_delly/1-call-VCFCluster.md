### VCFCluster
***
#### 前置step:
Module00c.PreprocessPESR
#### 作用范围：
for contig in contiglist
#### 测试样本:
+ HG00096
+ HG00129
#### 所用docker镜像：
ibio01:5000/cwhelan/sv-pipeline:cw_3c9d26c_single_sample_annotations
#### 所用脚本：
shard-0:
```xhsell
set -euo pipefail
for f in /.../std_000.delly.HG00096.vcf.gz /.../std_001.delly.HG00129.vcf.gz; do tabix -p vcf -f $f; done;
tabix -p bed /.../PESR.encode.peri_all.repeats.delly.hg38.blacklist.bed.gz;

svtk vcfcluster /.../write_lines_6b81a4376411661bbde08074a84f5b9f.tmp stdout \
  -r chr1 \
  -p ref_panel_1kg_v1_2tong_delly_chr1 \
  -d 300 \
  -f 0.1 \
  -x /.../PESR.encode.peri_all.repeats.delly.hg38.blacklist.bed.gz \
  -z 0 \
  -t DEL,DUP,INV,BND,INS \
  --preserve-ids \
  | vcf-sort -c \
  | bgzip -c > ref_panel_1kg_v1_2tong.delly.chr1.vcf.gz

```
#### 生成目录
所在目录：/home/user/zhangtong/gatksv_run/cromwell-executions/Module01/b645dd5f-151c-4284-a7e1-c4768000457e/call-ClusterPESR_delly/ClusterPESR/1bc8864a-d8e7-4edc-987f-1f00dde29331/call-VCFCluster/shard-0/execution

```
.
| -- docker_cid  
| -- ref_panel_1kg_v1_2tong.delly.chr1.vcf.gz  
| -- script.background  
| -- stderr             
| -- stdout             
| -- write_lines_6b81a4376411661bbde08074a84f5b9f.tmp
| -- rc          
| -- script                                    
| -- script.submit      
| -- stderr.background  
| -- stdout.background
```

#### 生成文件
```
ref_panel_1kg_v1_2tong.delly.chr1.vcf.gz
```