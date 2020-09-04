### BundledPostprocessGermlineCNVCalls
***
#### 前置step:
+ Module00c.gCNVCase.BundlePostprocessingInvariants
#### 作用范围：
for sample_index in range(length(counts))
#### 测试样本:
+ HG00096
+ HG00129
#### 所用docker镜像：
+ ibio01:5000/broadinstitute/gatk:4.1.2.0
#### 所用脚本：
```xhsell
set -euo pipefail

export GATK_LOCAL_JAR=/root/gatk.jar

# untar calls to CALLS_0, CALLS_1, etc directories and build the command line
# also copy over shard config and interval files
time tar xzf /.../case-gcnv-postprocessing-invariants.tar.gz
rm /.../case-gcnv-postprocessing-invariants.tar.gz
number_of_shards=`find . -name 'CALLS_*' | wc -l`

touch calls_and_model_args.txt
for i in $(seq 0 `expr $number_of_shards - 1`); do
    echo "--calls-shard-path CALLS_$i" >> calls_and_model_args.txt
    echo "--model-shard-path MODEL_$i" >> calls_and_model_args.txt
done

mkdir -p extracted-contig-ploidy-calls
tar xzf /.../case-contig-ploidy-calls.tar.gz -C extracted-contig-ploidy-calls
rm /.../case-contig-ploidy-calls.tar.gz

allosomal_contigs_args="--allosomal-contig chrX --allosomal-contig chrY"

time gatk --java-options "-Xmx8000m" PostprocessGermlineCNVCalls \
     --arguments_file calls_and_model_args.txt \
    $allosomal_contigs_args \
    --autosomal-ref-copy-number 2 \
    --contig-ploidy-calls extracted-contig-ploidy-calls \
    --sample-index 0 \
    --output-genotyped-intervals genotyped-intervals-HG00096.vcf.gz \
    --output-genotyped-segments genotyped-segments-HG00096.vcf.gz

rm -Rf extracted-contig-ploidy-calls
```

#### 生成目录
所在目录：/home/user/zhangtong/gatksv_run/cromwell-executions/Module00c/c473d627-53ec-45c1-a1c2-e3d4256e0f6c/call-gCNVCase/CNVGermlineCaseWorkflow/1768f03f-7b99-44cd-bfb0-ba6ab0941b4c/call-BundledPostprocessGermlineCNVCalls/shard-0/execution
```xml
.
├── CALLS_0
├── CALLS_1
├── CALLS_10
├── CALLS_100
├── CALLS_101
├── CALLS_102
├── CALLS_103
├── CALLS_104
├── CALLS_105
├── CALLS_106
├── CALLS_107
├── CALLS_108
├── CALLS_109
├── CALLS_11
├── CALLS_110
├── CALLS_111
├── CALLS_112
├── CALLS_113
├── CALLS_114
├── CALLS_115
├── CALLS_116
├── CALLS_117
├── CALLS_118
├── CALLS_119
├── CALLS_12
and so on.
```
#### 生成文件
```
在每个文件夹内
```