### DetermineGermlineContigPloidyCaseMode
***
#### 作用范围:
仅一次
#### 测试样本:
+ HG00096
+ HG00097
#### 所用docker镜像：
broadinstitute/gatk:4.1.2.0
#### 所用脚本：
测试:
```xhsell
cd /.../call-DetermineGermlineContigPloidyCaseMode/execution


set -euo pipefail
mkdir out
export GATK_LOCAL_JAR=/root/gatk.jar
export MKL_NUM_THREADS=4
export OMP_NUM_THREADS=4

mkdir input-contig-ploidy-model
tar xzf /.../call-DetermineGermlineContigPloidyCaseMode/inputs/-61350
6260/hg38_v0_sv-resources_ref-panel_1KG_v1_gcnv_1KGP_2504-contig-ploidy-model.tar -C input-contig-ploidy-model

read_count_files_list=/.../call-DetermineGermlineContigPloidyCaseMode
/execution/write_lines_6da2162e2ea3ca26946ebada9d515d79.tmp
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
#### 生成文件
```xml
.
├── case-contig-ploidy-calls.tar.gz
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
└── read_count_files.args
```