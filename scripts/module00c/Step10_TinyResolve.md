### TinyResolve
***
#### 前置step:
PreprocessPESR
#### 测试样本:
+ HG00096
+ HG00097
#### 所用docker镜像：
Todo
#### 所用脚本：
测试：
```xhsell
cd /call-TinyResolve/TinyResolve/8112d835-300d-414b-b3e9-d874cede0207/call-ResolveManta/shard-0/execution


set -euo pipefail
vcfs=(/cromwell-executions/GATKSVPipelinePhase1/981f6726-8b5d-4d6c-9842-5cac238846f0/call-Module00c/Module00c/cc9c6767-9427-47ae-8
87a-10c621dc8083/call-TinyResolve/TinyResolve/8112d835-300d-414b-b3e9-d874cede0207/call-ResolveManta/shard-0/inputs/685895020/std_
000.manta.HG00096.vcf.gz /cromwell-executions/GATKSVPipelinePhase1/981f6726-8b5d-4d6c-9842-5cac238846f0/call-Module00c/Module00c/c
c9c6767-9427-47ae-887a-10c621dc8083/call-TinyResolve/TinyResolve/8112d835-300d-414b-b3e9-d874cede0207/call-ResolveManta/shard-0/in
puts/685895020/std_001.manta.HG00097.vcf.gz)
sample_ids=(HG00096 HG00097)
discfiles=(/cromwell-executions/GATKSVPipelinePhase1/981f6726-8b5d-4d6c-9842-5cac238846f0/call-Module00c/Module00c/cc9c6767-9427-4
7ae-887a-10c621dc8083/call-TinyResolve/TinyResolve/8112d835-300d-414b-b3e9-d874cede0207/call-ResolveManta/shard-0/inputs/150263767
0/HG00096.chr22.disc.txt.gz /cromwell-executions/GATKSVPipelinePhase1/981f6726-8b5d-4d6c-9842-5cac238846f0/call-Module00c/Module00
c/cc9c6767-9427-47ae-887a-10c621dc8083/call-TinyResolve/TinyResolve/8112d835-300d-414b-b3e9-d874cede0207/call-ResolveManta/shard-0
/inputs/1502637670/HG00097.chr22.disc.txt.gz)
for (( i=0; i<2; i++ ));
do
  vcf=${vcfs[$i]}
  tabix -p vcf $vcf
  sample_id=${sample_ids[$i]}
  pe=${discfiles[$i]}
  sample_no=`printf %03d $i`
  bash /opt/sv-pipeline/00_preprocessing/scripts/mantatloccheck.sh $vcf $pe ${sample_id} /cromwell-executions/GATKSVPipelinePhase1
/981f6726-8b5d-4d6c-9842-5cac238846f0/call-Module00c/Module00c/cc9c6767-9427-47ae-887a-10c621dc8083/call-TinyResolve/TinyResolve/8
112d835-300d-414b-b3e9-d874cede0207/call-ResolveManta/shard-0/inputs/-1454618493/hg38_v0_sv-resources_resources_v1_mei_hg38.bed.gz
 /cromwell-executions/GATKSVPipelinePhase1/981f6726-8b5d-4d6c-9842-5cac238846f0/call-Module00c/Module00c/cc9c6767-9427-47ae-887a-1
0c621dc8083/call-TinyResolve/TinyResolve/8112d835-300d-414b-b3e9-d874cede0207/call-ResolveManta/shard-0/inputs/-1454618493/hg38_v0
_sv-resources_resources_v1_cytobands_hg38.bed.gz
  mv ${sample_id}.manta.complex.vcf.gz tloc_${sample_no}.${sample_id}.manta.complex.vcf.gz
done
```

#### 生成结果
```xml
.
├── docker_cid
├── glob-d76b2bc34052bb46ad61346e35709c3d
│   ├── cromwell_glob_control_file
│   ├── tloc_000.HG00096.manta.complex.vcf.gz
│   └── tloc_001.HG00097.manta.complex.vcf.gz
├── glob-d76b2bc34052bb46ad61346e35709c3d.list
├── manta.unresolved.vcf
├── manta.vcf.gz
├── manta.vcf.gz.tbi
├── rc
├── tloc_000.HG00096.manta.complex.vcf.gz
└── tloc_001.HG00097.manta.complex.vcf.gz

1 directory, 16 files
```