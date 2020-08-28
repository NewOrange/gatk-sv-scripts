# Manta

## 前置step
Step1_CramtoBam

## 所用docker镜像
`gatksv/manta:8645aa
`
## 测试bam
测试bam：HG00096

## 测试脚本
```shell
set -Eeuo pipefail

# if a preemptible instance restarts and runWorkflow.py already
# exists, manta will throw an error
if [ -f ./runWorkflow.py ]; then
  rm ./runWorkflow.py
fi

# prepare the analysis job
/usr/local/bin/manta/bin/configManta.py \
  --bam /cromwell-executions/GATKSVPipelineBatch/613a9504-0455-4088-a881-2b793b83ef44/call-Module00aBatch/Module00aBatch/6e2a710b-c9fc-4632-94fa
-e2f01eceabbd/call-Module00a/shard-0/Module00a/4ad015d9-2f0e-42c9-bf6f-e9d58604ee3a/call-Manta/Manta/799938f7-d414-46fb-82e4-0cbdcdcfb84b/call-R
unManta/inputs/-1297079738/HG00096.final.bam \
  --referenceFasta /cromwell-executions/GATKSVPipelineBatch/613a9504-0455-4088-a881-2b793b83ef44/call-Module00aBatch/Module00aBatch/6e2a710b-c9f
c-4632-94fa-e2f01eceabbd/call-Module00a/shard-0/Module00a/4ad015d9-2f0e-42c9-bf6f-e9d58604ee3a/call-Manta/Manta/799938f7-d414-46fb-82e4-0cbdcdcf
b84b/call-RunManta/inputs/-126943579/Homo_sapiens_assembly38.fasta \
  --runDir . \
  --callRegions /cromwell-executions/GATKSVPipelineBatch/613a9504-0455-4088-a881-2b793b83ef44/call-Module00aBatch/Module00aBatch/6e2a710b-c9fc-4
632-94fa-e2f01eceabbd/call-Module00a/shard-0/Module00a/4ad015d9-2f0e-42c9-bf6f-e9d58604ee3a/call-Manta/Manta/799938f7-d414-46fb-82e4-0cbdcdcfb84
b/call-RunManta/inputs/745429519/primary_contigs_plus_mito.bed.gz

# always tell manta there are 2 GiB per job, otherwise it will
# scale back the requested number of jobs, even if they won't
# need that much memory
./runWorkflow.py \
  --mode local \
  --jobs 10 \
  --memGb $((10 * 2))

# inversion conversion, then compression and index
python2 /usr/local/bin/manta/libexec/convertInversion.py \
  /usr/local/bin/samtools \
  /cromwell-executions/GATKSVPipelineBatch/613a9504-0455-4088-a881-2b793b83ef44/call-Module00aBatch/Module00aBatch/6e2a710b-c9fc-4632-94fa-e2f01
eceabbd/call-Module00a/shard-0/Module00a/4ad015d9-2f0e-42c9-bf6f-e9d58604ee3a/call-Manta/Manta/799938f7-d414-46fb-82e4-0cbdcdcfb84b/call-RunMant
a/inputs/-126943579/Homo_sapiens_assembly38.fasta \
  results/variants/diploidSV.vcf.gz \
  | bcftools reheader -s <(echo "HG00096") \
  > diploidSV.vcf

bgzip -c diploidSV.vcf > HG00096.manta.vcf.gz
tabix -p vcf HG00096.manta.vcf.gz
```
## 测试目录
所在目录：/home/user/zhangtong/gatksv_run/cromwell-executions/GATKSVPipelineBatch/613a9504-0455-4088-a881-2b793b83ef44/call-Module00aBatch/Module00aBatch/6e2a710b-c9fc-4632-94fa-e2f01eceabbd/call-Module00a/shard-0/Module00a/4ad015d9-2f0e-42c9-bf6f-e9d58604ee3a/call-Manta/Manta/799938f7-d414-46fb-82e4-0cbdcdcfb84b/call-RunManta/execution
```xml
.
├── diploidSV.vcf
├── docker_cid
├── HG00096.manta.vcf.gz
├── HG00096.manta.vcf.gz.tbi
├── rc
├── results
│   ├── evidence
│   ├── stats
│   └── variants
├── runWorkflow.py
├── runWorkflow.py.config.pickle
├── script
├── script.background
├── script.submit
├── stderr
├── stderr.background
├── stdout
├── stdout.background
├── workflow.error.log.txt
├── workflow.exitcode.txt
├── workflow.warning.log.txt
└── workspace
    ├── alignmentStats.xml
    ├── chromDepth.txt
    ├── edgeRuntimeLog.txt
    ├── pyflow.data
    ├── svHyGen
    └── svLocusGraph.bin
```
## 生成文件
```
HG00096.manta.vcf.gz
HG00096.manta.vcf.gz.tbi
```