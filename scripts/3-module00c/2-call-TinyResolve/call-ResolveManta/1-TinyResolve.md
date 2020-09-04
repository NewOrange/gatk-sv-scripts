### TinyResolve
***
#### 前置step:
Module00c.PreprocessPESR
#### 运行条件：
manta_vcf
#### 测试样本:
+ HG00096
+ HG00129
#### 所用docker镜像：
ibio01:5000/cwhelan/sv-pipeline:cw_3c9d26c_single_sample_annotations
#### 所用脚本：
测试：
```xhsell
set -euo pipefail
vcfs=(/.../std_000.manta.HG00096.vcf.gz /.../std_001.manta.HG00129.vcf.gz)
sample_ids=(HG00096 HG00129)
discfiles=(/.../HG00096.disc.txt.gz /.../HG00129.disc.txt.gz)
for (( i=0; i<2; i++ ));
do
  vcf=${vcfs[$i]}
  tabix -p vcf $vcf
  sample_id=${sample_ids[$i]}
  pe=${discfiles[$i]}
  sample_no=`printf %03d $i`
  bash /opt/sv-pipeline/00_preprocessing/scripts/mantatloccheck.sh $vcf $pe ${sample_id} /.../mei_hg38.bed.gz /.../cytobands_hg38.bed.gz
  mv ${sample_id}.manta.complex.vcf.gz tloc_${sample_no}.${sample_id}.manta.complex.vcf.gz
done
```

#### 生成目录

所在目录：/home/user/zhangtong/gatksv_run/cromwell-executions/Module00c/9689f669-dda1-40b4-a6df-aa35c9d84202/call-TinyResolve/TinyResolve/af11376c-d6e8-4635-8848-6fcc99894780/call-ResolveManta/shard-0/execution

```xml
.
├── docker_cid
├── glob-d76b2bc34052bb46ad61346e35709c3d
│   └── cromwell_glob_control_file
├── glob-d76b2bc34052bb46ad61346e35709c3d.list
├── manta.unresolved.vcf
├── manta.vcf.gz
├── manta.vcf.gz.tbi
├── rc
├── script
├── script.background
├── script.submit
├── stderr
├── stderr.background
├── stdout
├── stdout.background
├── tloc_000.HG00096.manta.complex.vcf.gz
└── tloc_001.HG00129.manta.complex.vcf.gz

1 directory, 16 files
```
#### 生成文件
```
manta.unresolved.vcf
manta.vcf.gz
manta.vcf.gz.tbi
tloc_000.HG00096.manta.complex.vcf.gz
tloc_001.HG00129.manta.complex.vcf.gz
```