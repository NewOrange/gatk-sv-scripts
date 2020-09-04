### StandardizeVCFs
***
#### 前置step:
Module00aBatch
#### 作用范围
for i in i in range(length(algorithms)
#### 测试样本:
+ HG00096
+ HG00129
#### 所用docker镜像：
+ ibio01:5000/cwhelan/sv-pipeline:cw_3c9d26c_single_sample_annotations
#### 所用脚本：
manta(shard-0)：
```xhsell
set -euo pipefail
vcfs=(/.../HG00096.manta.vcf.gz /.../HG00129.manta.vcf.gz)
sample_ids=(HG00096 HG00129)
for (( i=0; i<2; i++ ));
do
  vcf=${vcfs[$i]}
  sample_id=${sample_ids[$i]}
  sample_no=`printf %03d $i`
  svtk standardize --sample-names ${sample_id} --prefix manta_${sample_id} --contigs /.../contig.fai --min-size 50 $vcf manta.${sample_id}_unsorted.vcf manta
  vcf-sort -c manta.${sample_id}_unsorted.vcf | bgzip -c > std_${sample_no}.manta.${sample_id}.vcf.gz
done
```
#### 生成结果
shard-0：
所在目录：/home/user/zhangtong/gatksv_run/cromwell-executions/Module00c/c473d627-53ec-45c1-a1c2-e3d4256e0f6c/call-PreprocessPESR/PreprocessPESR/531a3eac-0bb8-4d3f-996f-7a177ac3e206/call-StandardizeVCFs/shard-0/execution
```xml
.
├── docker_cid
├── glob-31de091d1940ddb276ce7b6086a74725
│   └── cromwell_glob_control_file
├── glob-31de091d1940ddb276ce7b6086a74725.list
├── manta.HG00096_unsorted.vcf
├── manta.HG00129_unsorted.vcf
├── rc
├── script
├── script.background
├── script.submit
├── std_000.manta.HG00096.vcf.gz
├── std_001.manta.HG00129.vcf.gz
├── stderr
├── stderr.background
├── stdout
└── stdout.background

1 directory, 15 files
```
#### 生成文件
```
std_000.manta.HG00096.vcf.gz
std_001.manta.HG00129.vcf.gz
```