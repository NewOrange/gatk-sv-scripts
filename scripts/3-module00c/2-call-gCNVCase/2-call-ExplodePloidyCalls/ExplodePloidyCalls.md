### ExplodePloidyCalls
***
#### 前置step:
+ Module00c.gCNVCase.GermlineCNVCallerCaseModeDetermineGermlineContigPloidyCaseMode
#### 作用范围：
仅一次
#### 测试样本:
+ HG00096
+ HG00129
#### 所用docker镜像：
+ ibio01:5000/broadinstitute/gatk:4.1.2.0
#### 所用脚本：
```xhsell
set -euo pipefail
mkdir out
export GATK_LOCAL_JAR=/root/gatk.jar
export MKL_NUM_THREADS=4
export OMP_NUM_THREADS=4

mkdir input-contig-ploidy-model
tar xzf /.../1KGP_2504-contig-ploidy-model.tar.gz -C input-contig-ploidy-model

read_count_files_list=/.../write_lines_abe21bd2c6643c269d61011b16be71aa.tmp
grep gz$ $read_count_files_list | xargs -l1 -P0 gunzip
sed 's/\.gz$//' $read_count_files_list | \
    awk '{print "--input "$0}' > read_count_files.args

gatk --java-options "-Xmx8000m" DetermineGermlineContigPloidy \
    --arguments_file read_count_files.args \
    --model input-contig-ploidy-model \
    --output out \
    --output-prefix case \
    --verbosity DEBUG \
    --mapping-error-rate 0.01 \
    --sample-psi-scale 0.0001

tar c -C out/case-calls . | gzip -1 > case-contig-ploidy-calls.tar.gz
```

#### 生成目录
所在目录：/home/user/zhangtong/gatksv_run/cromwell-executions/Module00c/c473d627-53ec-45c1-a1c2-e3d4256e0f6c/call-gCNVCase/CNVGermlineCaseWorkflow/1768f03f-7b99-44cd-bfb0-ba6ab0941b4c/call-DetermineGermlineContigPloidyCaseMode/execution
```xml
.
├── case-contig-ploidy-calls.tar.gz
├── docker_cid
├── input-contig-ploidy-model
│   ├── contig_ploidy_prior.tsv
│   ├── gcnvkernel_version.json
│   ├── interval_list.tsv
│   ├── mu_mean_bias_j_lowerbound__.tsv
│   ├── mu_psi_j_log__.tsv
│   ├── ploidy_config.json
│   ├── std_mean_bias_j_lowerbound__.tsv
│   └── std_psi_j_log__.tsv
├── out
│   └── case-calls
│       ├── SAMPLE_0
│       │   ├── contig_ploidy.tsv
│       │   ├── global_read_depth.tsv
│       │   ├── mu_psi_s_log__.tsv
│       │   ├── sample_name.txt
│       │   └── std_psi_s_log__.tsv
│       └── SAMPLE_1
│           ├── contig_ploidy.tsv
│           ├── global_read_depth.tsv
│           ├── mu_psi_s_log__.tsv
│           ├── sample_name.txt
│           └── std_psi_s_log__.tsv
├── rc
├── read_count_files.args
├── script
├── script.background
├── script.submit
├── stderr
├── stderr.background
├── stdout
├── stdout.background
└── write_lines_abe21bd2c6643c269d61011b16be71aa.tmp

5 directories, 30 files
```
#### 生成文件
```
case-contig-ploidy-calls.tar.gz
```