### PreprocessPESR
***
#### 前置step:
Todo
#### 测试样本:
+ HG00096
+ HG00097
#### 所用docker镜像：
Todo
#### 所用脚本：
测试：
```xhsell
cd /.../shard-0/execution


set -euo pipefail
vcfs=(/cromwell-executions/GATKSVPipelinePhase1/8d210b54-725e-47f8-aa63-3c21b9aa8f31/call-Module00c/Module00c/b362d99d-0e0b-47a8-8
322-c6bd753e915f/call-PreprocessPESR/PreprocessPESR/4f5ae3b2-6979-4510-aed7-480ac4a5ebc6/call-StandardizeVCFs/shard-0/inputs/15026
37669/HG00096.chr22.manta.vcf.gz /cromwell-executions/GATKSVPipelinePhase1/8d210b54-725e-47f8-aa63-3c21b9aa8f31/call-Module00c/Mod
ule00c/b362d99d-0e0b-47a8-8322-c6bd753e915f/call-PreprocessPESR/PreprocessPESR/4f5ae3b2-6979-4510-aed7-480ac4a5ebc6/call-Standardi
zeVCFs/shard-0/inputs/1502637669/HG00097.chr22.manta.vcf.gz)
sample_ids=(HG00096 HG00097)
for (( i=0; i<2; i++ ));
do
  vcf=${vcfs[$i]}
  sample_id=${sample_ids[$i]}
  sample_no=`printf %03d $i`
  svtk standardize --sample-names ${sample_id} --prefix manta_${sample_id} --contigs /cromwell-executions/GATKSVPipelinePhase1/8d2
10b54-725e-47f8-aa63-3c21b9aa8f31/call-Module00c/Module00c/b362d99d-0e0b-47a8-8322-c6bd753e915f/call-PreprocessPESR/PreprocessPESR
/4f5ae3b2-6979-4510-aed7-480ac4a5ebc6/call-StandardizeVCFs/shard-0/inputs/-1454618493/hg38_v0_sv-resources_resources_v1_contig.fai
 --min-size 50 $vcf manta.${sample_id}_unsorted.vcf manta
  vcf-sort -c manta.${sample_id}_unsorted.vcf | bgzip -c > std_${sample_no}.manta.${sample_id}.vcf.gz
done
```
shard-1
```shell
cd /.../shard-1/execution


set -euo pipefail
vcfs=(/cromwell-executions/GATKSVPipelinePhase1/8d210b54-725e-47f8-aa63-3c21b9aa8f31/call-Module00c/Module00c/b362d99d-0e0b-47a8-8
322-c6bd753e915f/call-PreprocessPESR/PreprocessPESR/4f5ae3b2-6979-4510-aed7-480ac4a5ebc6/call-StandardizeVCFs/shard-1/inputs/15026
37672/HG00096.chr22.delly.vcf.gz /cromwell-executions/GATKSVPipelinePhase1/8d210b54-725e-47f8-aa63-3c21b9aa8f31/call-Module00c/Mod
ule00c/b362d99d-0e0b-47a8-8322-c6bd753e915f/call-PreprocessPESR/PreprocessPESR/4f5ae3b2-6979-4510-aed7-480ac4a5ebc6/call-Standardi
zeVCFs/shard-1/inputs/1502637672/HG00097.chr22.delly.vcf.gz)
sample_ids=(HG00096 HG00097)
for (( i=0; i<2; i++ ));
do
  vcf=${vcfs[$i]}
  sample_id=${sample_ids[$i]}
  sample_no=`printf %03d $i`
  svtk standardize --sample-names ${sample_id} --prefix delly_${sample_id} --contigs /cromwell-executions/GATKSVPipelinePhase1/8d2
10b54-725e-47f8-aa63-3c21b9aa8f31/call-Module00c/Module00c/b362d99d-0e0b-47a8-8322-c6bd753e915f/call-PreprocessPESR/PreprocessPESR
/4f5ae3b2-6979-4510-aed7-480ac4a5ebc6/call-StandardizeVCFs/shard-1/inputs/-1454618493/hg38_v0_sv-resources_resources_v1_contig.fai
 --min-size 50 $vcf delly.${sample_id}_unsorted.vcf delly
  vcf-sort -c delly.${sample_id}_unsorted.vcf | bgzip -c > std_${sample_no}.delly.${sample_id}.vcf.gz
done
```
#### 生成结果
shard-0
```xml
.
├── glob-31de091d1940ddb276ce7b6086a74725
│   ├── cromwell_glob_control_file
│   ├── std_000.manta.HG00096.vcf.gz
│   └── std_001.manta.HG00097.vcf.gz
├── glob-31de091d1940ddb276ce7b6086a74725.list
├── manta.HG00096_unsorted.vcf
├── manta.HG00097_unsorted.vcf
├── rc
├── std_000.manta.HG00096.vcf.gz
└── std_001.manta.HG00097.vcf.gz

1 directory, 17 files
```
shard-1
```xml
.
├── delly.HG00096_unsorted.vcf
├── delly.HG00097_unsorted.vcf
├── glob-31de091d1940ddb276ce7b6086a74725
│   ├── cromwell_glob_control_file
│   ├── std_000.delly.HG00096.vcf.gz
│   └── std_001.delly.HG00097.vcf.gz
├── glob-31de091d1940ddb276ce7b6086a74725.list
├── rc
├── std_000.delly.HG00096.vcf.gz
└── std_001.delly.HG00097.vcf.gz

1 directory, 17 files
```
Summary:
```json
{
  "PreprocessPESR.std_manta_vcf": ["/.../shard-0/execution/glob-31de091d1940ddb276ce7b6086a74725/std_000.manta.HG00096.vcf.gz", "/.../shard-0/execution/glob-31de091d1940ddb276ce7b6086a74725/std_001.manta.HG00097.vcf.gz"],
  "PreprocessPESR.std_wham_vcf": null,
  "PreprocessPESR.std_melt_vcf": null,
  "PreprocessPESR.std_delly_vcf": ["/.../shard-1/execution/glob-31de091d1940ddb276ce7b6086a74725/std_000.delly.HG00096.vcf.gz", "/.../shard-1/execution/glob-31de091d1940ddb276ce7b6086a74725/std_001.delly.HG00097.vcf.gz"]
}
```