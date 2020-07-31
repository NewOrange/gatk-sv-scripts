### GermlineCNVCallerCaseMode
***
#### 作用范围:
for scatter_index in range(length(gcnv_model_tars)
#### 测试样本:
+ HG00096
+ HG00097
#### 所用docker镜像：
broadinstitute/gatk:4.1.2.0
#### 所用脚本：
测试:
shard-0:
```xhsell
cd /.../call-GermlineCNVCallerCaseMode/shard-0/execution


set -euo pipefail
mkdir out
export GATK_LOCAL_JAR=/root/gatk.jar
export MKL_NUM_THREADS=4
export OMP_NUM_THREADS=4

mkdir contig-ploidy-calls-dir
tar xzf /.../call-GermlineCNVCallerCaseMode/shard-0/inputs/2136129407
/case-contig-ploidy-calls.tar.gz -C contig-ploidy-calls-dir

mkdir gcnv-model
tar xzf /.../call-GermlineCNVCallerCaseMode/shard-0/inputs/1321039322
/hg38_v0_sv-resources_ref-panel_1KG_gcnv_case-gcnv-model-files-0.tar.gz -C gcnv-model

read_count_files_list=/.../call-GermlineCNVCallerCaseMode/shard-0/exe
cution/write_lines_2bda6c984b6f7a97657d4f1ed40e1962.tmp
grep gz$ $read_count_files_list | xargs -l1 -P0 gunzip
sed 's/\.gz$//' $read_count_files_list | \
    awk '{print "--input "$0}' > read_count_files.args

gatk --java-options "-Xmx9500m"  GermlineCNVCaller \
    --run-mode CASE \
    --arguments_file read_count_files.args \
    --contig-ploidy-calls contig-ploidy-calls-dir \
    --model gcnv-model \
    --output out \
    --output-prefix case \
    --verbosity DEBUG \
    --p-alt 1.0E-6 \
    --cnv-coherence-length 1000.0 \
    --max-copy-number 5 \
    --mapping-error-rate 0.01 \
    --sample-psi-scale 1.0E-6 \
    --depth-correction-tau 10000.0 \
    --copy-number-posterior-expectation-mode EXACT \
    --active-class-padding-hybrid-mode 50000 \
    --learning-rate 0.03 \
    --adamax-beta-1 0.9 \
    --adamax-beta-2 0.99 \
    --log-emission-samples-per-round 50 \
    --log-emission-sampling-median-rel-error 0.001 \
    --log-emission-sampling-rounds 20 \
    --max-advi-iter-first-epoch 1000 \
    --max-advi-iter-subsequent-epochs 200 \
    --min-training-epochs 1 \
    --max-training-epochs 5 \
    --initial-temperature 2.0 \
    --num-thermal-advi-iters 250 \
    --convergence-snr-averaging-window 100 \
    --convergence-snr-trigger-threshold 0.2 \
    --convergence-snr-countdown-window 10 \
    --max-calling-iters 10 \
    --caller-update-convergence-threshold 1.0E-6 \
    --caller-internal-admixing-rate 0.5 \
    --caller-external-admixing-rate 1.00 \
    --disable-annealing false

tar c -C out/case-tracking . | gzip -1 > case-gcnv-tracking-0.tar.gz
tar c -C out/case-calls  . | gzip -1 > case-gcnv-calls-files-0.tar.gz
```
#### 生成文件
shard-0:
```xml
.
├── case-gcnv-calls-files-0.tar.gz
├── case-gcnv-tracking-0.tar.gz
├── contig-ploidy-calls-dir
│   ├── SAMPLE_0
│   │   ├── contig_ploidy.tsv
│   │   ├── global_read_depth.tsv
│   │   ├── mu_psi_s_log__.tsv
│   │   ├── sample_name.txt
│   │   └── std_psi_s_log__.tsv
│   └── SAMPLE_1
│       ├── contig_ploidy.tsv
│       ├── global_read_depth.tsv
│       ├── mu_psi_s_log__.tsv
│       ├── sample_name.txt
│       └── std_psi_s_log__.tsv
├── gcnv-model
│   ├── calling_config.json
│   ├── denoising_config.json
│   ├── gcnvkernel_version.json
│   ├── interval_list.tsv
│   ├── log_q_tau_tk.tsv
│   ├── mu_log_mean_bias_t.tsv
│   ├── mu_psi_t_log__.tsv
│   ├── std_log_mean_bias_t.tsv
│   └── std_psi_t_log__.tsv
├── out
│   ├── case-calls
│   │   ├── calling_config.json
│   │   ├── denoising_config.json
│   │   ├── gcnvkernel_version.json
│   │   ├── interval_list.tsv
│   │   ├── SAMPLE_0
│   │   │   ├── baseline_copy_number_t.tsv
│   │   │   ├── log_c_emission_tc.tsv
│   │   │   ├── log_q_c_tc.tsv
│   │   │   ├── mu_denoised_copy_ratio_t.tsv
│   │   │   ├── mu_psi_s_log__.tsv
│   │   │   ├── mu_read_depth_s_log__.tsv
│   │   │   ├── mu_z_sg.tsv
│   │   │   ├── sample_name.txt
│   │   │   ├── std_denoised_copy_ratio_t.tsv
│   │   │   ├── std_psi_s_log__.tsv
│   │   │   ├── std_read_depth_s_log__.tsv
│   │   │   └── std_z_sg.tsv
│   │   └── SAMPLE_1
│   │       ├── baseline_copy_number_t.tsv
│   │       ├── log_c_emission_tc.tsv
│   │       ├── log_q_c_tc.tsv
│   │       ├── mu_denoised_copy_ratio_t.tsv
│   │       ├── mu_psi_s_log__.tsv
│   │       ├── mu_read_depth_s_log__.tsv
│   │       ├── mu_z_sg.tsv
│   │       ├── sample_name.txt
│   │       ├── std_denoised_copy_ratio_t.tsv
│   │       ├── std_psi_s_log__.tsv
│   │       ├── std_read_depth_s_log__.tsv
│   │       └── std_z_sg.tsv
│   └── case-tracking
│       └── elbo_history.tsv
├── read_count_files.args
└── write_lines_2bda6c984b6f7a97657d4f1ed40e1962.tmp
```