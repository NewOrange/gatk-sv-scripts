### BundledPostprocessGermlineCNVCalls
***
#### 作用范围:
for sample_index in range(length(counts))
#### 测试样本:
+ HG00096
+ HG00097
#### 所用docker镜像：
broadinstitute/gatk:4.1.2.0
#### 所用脚本：
测试:
shard-0:
```xhsell
cd /.../call-BundledPostprocessGermlineCNVCalls/shard-0/execution


set -euo pipefail

export GATK_LOCAL_JAR=/root/gatk.jar

# untar calls to CALLS_0, CALLS_1, etc directories and build the command line
# also copy over shard config and interval files
time tar xzf /.../call-BundledPostprocessGermlineCNVCalls/shard-0/inp
uts/516310921/case-gcnv-postprocessing-invariants.tar.gz
rm /.../call-BundledPostprocessGermlineCNVCalls/shard-0/inputs/516310
921/case-gcnv-postprocessing-invariants.tar.gz
number_of_shards=`find . -name 'CALLS_*' | wc -l`

touch calls_and_model_args.txt
for i in $(seq 0 `expr $number_of_shards - 1`); do
    echo "--calls-shard-path CALLS_$i" >> calls_and_model_args.txt
    echo "--model-shard-path MODEL_$i" >> calls_and_model_args.txt
done

mkdir -p extracted-contig-ploidy-calls
tar xzf /.../call-BundledPostprocessGermlineCNVCalls/shard-0/inputs/2
136129407/case-contig-ploidy-calls.tar.gz -C extracted-contig-ploidy-calls
rm /.../call-BundledPostprocessGermlineCNVCalls/shard-0/inputs/213612
9407/case-contig-ploidy-calls.tar.gz

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
#### 生成文件
shard-0:
```xml

.
├── CALLS_0
│   ├── calling_config.json
│   ├── denoising_config.json
│   ├── gcnvkernel_version.json
│   ├── interval_list.tsv
│   ├── SAMPLE_0
│   │   ├── baseline_copy_number_t.tsv
│   │   ├── log_c_emission_tc.tsv
│   │   ├── log_q_c_tc.tsv
│   │   ├── mu_denoised_copy_ratio_t.tsv
│   │   ├── mu_psi_s_log__.tsv
│   │   ├── mu_read_depth_s_log__.tsv
│   │   ├── mu_z_sg.tsv
│   │   ├── sample_name.txt
│   │   ├── std_denoised_copy_ratio_t.tsv
│   │   ├── std_psi_s_log__.tsv
│   │   ├── std_read_depth_s_log__.tsv
│   │   └── std_z_sg.tsv
│   └── SAMPLE_1
│       ├── baseline_copy_number_t.tsv
│       ├── log_c_emission_tc.tsv
│       ├── log_q_c_tc.tsv
│       ├── mu_denoised_copy_ratio_t.tsv
│       ├── mu_psi_s_log__.tsv
│       ├── mu_read_depth_s_log__.tsv
│       ├── mu_z_sg.tsv
│       ├── sample_name.txt
│       ├── std_denoised_copy_ratio_t.tsv
│       ├── std_psi_s_log__.tsv
│       ├── std_read_depth_s_log__.tsv
│       └── std_z_sg.tsv
├── CALLS_1
│   ├── calling_config.json
│   ├── denoising_config.json
│   ├── gcnvkernel_version.json
│   ├── interval_list.tsv
│   ├── SAMPLE_0
│   │   ├── baseline_copy_number_t.tsv
│   │   ├── log_c_emission_tc.tsv
│   │   ├── log_q_c_tc.tsv
│   │   ├── mu_denoised_copy_ratio_t.tsv
│   │   ├── mu_psi_s_log__.tsv
│   │   ├── mu_read_depth_s_log__.tsv
│   │   ├── mu_z_sg.tsv
│   │   ├── sample_name.txt
│   │   ├── std_denoised_copy_ratio_t.tsv
│   │   ├── std_psi_s_log__.tsv
│   │   ├── std_read_depth_s_log__.tsv
│   │   └── std_z_sg.tsv
│   └── SAMPLE_1
│       ├── baseline_copy_number_t.tsv
│       ├── log_c_emission_tc.tsv
│       ├── log_q_c_tc.tsv
│       ├── mu_denoised_copy_ratio_t.tsv
│       ├── mu_psi_s_log__.tsv
│       ├── mu_read_depth_s_log__.tsv
│       ├── mu_z_sg.tsv
│       ├── sample_name.txt
│       ├── std_denoised_copy_ratio_t.tsv
│       ├── std_psi_s_log__.tsv
│       ├── std_read_depth_s_log__.tsv
│       └── std_z_sg.tsv
├── CALLS_10
│   ├── calling_config.json
│   ├── denoising_config.json
│   ├── gcnvkernel_version.json
│   ├── interval_list.tsv
│   ├── SAMPLE_0
│   │   ├── baseline_copy_number_t.tsv
│   │   ├── log_c_emission_tc.tsv
│   │   ├── log_q_c_tc.tsv
│   │   ├── mu_denoised_copy_ratio_t.tsv
│   │   ├── mu_psi_s_log__.tsv
│   │   ├── mu_read_depth_s_log__.tsv
│   │   ├── mu_z_sg.tsv
│   │   ├── sample_name.txt
│   │   ├── std_denoised_copy_ratio_t.tsv
│   │   ├── std_psi_s_log__.tsv
│   │   ├── std_read_depth_s_log__.tsv
│   │   └── std_z_sg.tsv
│   └── SAMPLE_1
│       ├── baseline_copy_number_t.tsv
│       ├── log_c_emission_tc.tsv
│       ├── log_q_c_tc.tsv
│       ├── mu_denoised_copy_ratio_t.tsv
│       ├── mu_psi_s_log__.tsv
│       ├── mu_read_depth_s_log__.tsv
│       ├── mu_z_sg.tsv
│       ├── sample_name.txt
│       ├── std_denoised_copy_ratio_t.tsv
│       ├── std_psi_s_log__.tsv
│       ├── std_read_depth_s_log__.tsv
│       └── std_z_sg.tsv
├── CALLS_11
│   ├── calling_config.json
│   ├── denoising_config.json
│   ├── gcnvkernel_version.json
│   ├── interval_list.tsv
│   ├── SAMPLE_0
│   │   ├── baseline_copy_number_t.tsv
│   │   ├── log_c_emission_tc.tsv
│   │   ├── log_q_c_tc.tsv
│   │   ├── mu_denoised_copy_ratio_t.tsv
│   │   ├── mu_psi_s_log__.tsv
│   │   ├── mu_read_depth_s_log__.tsv
│   │   ├── mu_z_sg.tsv
│   │   ├── sample_name.txt
│   │   ├── std_denoised_copy_ratio_t.tsv
│   │   ├── std_psi_s_log__.tsv
│   │   ├── std_read_depth_s_log__.tsv
│   │   └── std_z_sg.tsv
│   └── SAMPLE_1
│       ├── baseline_copy_number_t.tsv
│       ├── log_c_emission_tc.tsv
│       ├── log_q_c_tc.tsv
│       ├── mu_denoised_copy_ratio_t.tsv
│       ├── mu_psi_s_log__.tsv
│       ├── mu_read_depth_s_log__.tsv
│       ├── mu_z_sg.tsv
│       ├── sample_name.txt
│       ├── std_denoised_copy_ratio_t.tsv
│       ├── std_psi_s_log__.tsv
│       ├── std_read_depth_s_log__.tsv
│       └── std_z_sg.tsv
├── CALLS_12
│   ├── calling_config.json
│   ├── denoising_config.json
│   ├── gcnvkernel_version.json
│   ├── interval_list.tsv
│   ├── SAMPLE_0
│   │   ├── baseline_copy_number_t.tsv
│   │   ├── log_c_emission_tc.tsv
│   │   ├── log_q_c_tc.tsv
│   │   ├── mu_denoised_copy_ratio_t.tsv
│   │   ├── mu_psi_s_log__.tsv
│   │   ├── mu_read_depth_s_log__.tsv
│   │   ├── mu_z_sg.tsv
│   │   ├── sample_name.txt
│   │   ├── std_denoised_copy_ratio_t.tsv
│   │   ├── std_psi_s_log__.tsv
│   │   ├── std_read_depth_s_log__.tsv
│   │   └── std_z_sg.tsv
│   └── SAMPLE_1
│       ├── baseline_copy_number_t.tsv
│       ├── log_c_emission_tc.tsv
│       ├── log_q_c_tc.tsv
│       ├── mu_denoised_copy_ratio_t.tsv
│       ├── mu_psi_s_log__.tsv
│       ├── mu_read_depth_s_log__.tsv
│       ├── mu_z_sg.tsv
│       ├── sample_name.txt
│       ├── std_denoised_copy_ratio_t.tsv
│       ├── std_psi_s_log__.tsv
│       ├── std_read_depth_s_log__.tsv
│       └── std_z_sg.tsv
├── CALLS_2
│   ├── calling_config.json
│   ├── denoising_config.json
│   ├── gcnvkernel_version.json
│   ├── interval_list.tsv
│   ├── SAMPLE_0
│   │   ├── baseline_copy_number_t.tsv
│   │   ├── log_c_emission_tc.tsv
│   │   ├── log_q_c_tc.tsv
│   │   ├── mu_denoised_copy_ratio_t.tsv
│   │   ├── mu_psi_s_log__.tsv
│   │   ├── mu_read_depth_s_log__.tsv
│   │   ├── mu_z_sg.tsv
│   │   ├── sample_name.txt
│   │   ├── std_denoised_copy_ratio_t.tsv
│   │   ├── std_psi_s_log__.tsv
│   │   ├── std_read_depth_s_log__.tsv
│   │   └── std_z_sg.tsv
│   └── SAMPLE_1
│       ├── baseline_copy_number_t.tsv
│       ├── log_c_emission_tc.tsv
│       ├── log_q_c_tc.tsv
│       ├── mu_denoised_copy_ratio_t.tsv
│       ├── mu_psi_s_log__.tsv
│       ├── mu_read_depth_s_log__.tsv
│       ├── mu_z_sg.tsv
│       ├── sample_name.txt
│       ├── std_denoised_copy_ratio_t.tsv
│       ├── std_psi_s_log__.tsv
│       ├── std_read_depth_s_log__.tsv
│       └── std_z_sg.tsv
├── CALLS_3
│   ├── calling_config.json
│   ├── denoising_config.json
│   ├── gcnvkernel_version.json
│   ├── interval_list.tsv
│   ├── SAMPLE_0
│   │   ├── baseline_copy_number_t.tsv
│   │   ├── log_c_emission_tc.tsv
│   │   ├── log_q_c_tc.tsv
│   │   ├── mu_denoised_copy_ratio_t.tsv
│   │   ├── mu_psi_s_log__.tsv
│   │   ├── mu_read_depth_s_log__.tsv
│   │   ├── mu_z_sg.tsv
│   │   ├── sample_name.txt
│   │   ├── std_denoised_copy_ratio_t.tsv
│   │   ├── std_psi_s_log__.tsv
│   │   ├── std_read_depth_s_log__.tsv
│   │   └── std_z_sg.tsv
│   └── SAMPLE_1
│       ├── baseline_copy_number_t.tsv
│       ├── log_c_emission_tc.tsv
│       ├── log_q_c_tc.tsv
│       ├── mu_denoised_copy_ratio_t.tsv
│       ├── mu_psi_s_log__.tsv
│       ├── mu_read_depth_s_log__.tsv
│       ├── mu_z_sg.tsv
│       ├── sample_name.txt
│       ├── std_denoised_copy_ratio_t.tsv
│       ├── std_psi_s_log__.tsv
│       ├── std_read_depth_s_log__.tsv
│       └── std_z_sg.tsv
├── CALLS_4
│   ├── calling_config.json
│   ├── denoising_config.json
│   ├── gcnvkernel_version.json
│   ├── interval_list.tsv
│   ├── SAMPLE_0
│   │   ├── baseline_copy_number_t.tsv
│   │   ├── log_c_emission_tc.tsv
│   │   ├── log_q_c_tc.tsv
│   │   ├── mu_denoised_copy_ratio_t.tsv
│   │   ├── mu_psi_s_log__.tsv
│   │   ├── mu_read_depth_s_log__.tsv
│   │   ├── mu_z_sg.tsv
│   │   ├── sample_name.txt
│   │   ├── std_denoised_copy_ratio_t.tsv
│   │   ├── std_psi_s_log__.tsv
│   │   ├── std_read_depth_s_log__.tsv
│   │   └── std_z_sg.tsv
│   └── SAMPLE_1
│       ├── baseline_copy_number_t.tsv
│       ├── log_c_emission_tc.tsv
│       ├── log_q_c_tc.tsv
│       ├── mu_denoised_copy_ratio_t.tsv
│       ├── mu_psi_s_log__.tsv
│       ├── mu_read_depth_s_log__.tsv
│       ├── mu_z_sg.tsv
│       ├── sample_name.txt
│       ├── std_denoised_copy_ratio_t.tsv
│       ├── std_psi_s_log__.tsv
│       ├── std_read_depth_s_log__.tsv
│       └── std_z_sg.tsv
├── CALLS_5
│   ├── calling_config.json
│   ├── denoising_config.json
│   ├── gcnvkernel_version.json
│   ├── interval_list.tsv
│   ├── SAMPLE_0
│   │   ├── baseline_copy_number_t.tsv
│   │   ├── log_c_emission_tc.tsv
│   │   ├── log_q_c_tc.tsv
│   │   ├── mu_denoised_copy_ratio_t.tsv
│   │   ├── mu_psi_s_log__.tsv
│   │   ├── mu_read_depth_s_log__.tsv
│   │   ├── mu_z_sg.tsv
│   │   ├── sample_name.txt
│   │   ├── std_denoised_copy_ratio_t.tsv
│   │   ├── std_psi_s_log__.tsv
│   │   ├── std_read_depth_s_log__.tsv
│   │   └── std_z_sg.tsv
│   └── SAMPLE_1
│       ├── baseline_copy_number_t.tsv
│       ├── log_c_emission_tc.tsv
│       ├── log_q_c_tc.tsv
│       ├── mu_denoised_copy_ratio_t.tsv
│       ├── mu_psi_s_log__.tsv
│       ├── mu_read_depth_s_log__.tsv
│       ├── mu_z_sg.tsv
│       ├── sample_name.txt
│       ├── std_denoised_copy_ratio_t.tsv
│       ├── std_psi_s_log__.tsv
│       ├── std_read_depth_s_log__.tsv
│       └── std_z_sg.tsv
├── CALLS_6
│   ├── calling_config.json
│   ├── denoising_config.json
│   ├── gcnvkernel_version.json
│   ├── interval_list.tsv
│   ├── SAMPLE_0
│   │   ├── baseline_copy_number_t.tsv
│   │   ├── log_c_emission_tc.tsv
│   │   ├── log_q_c_tc.tsv
│   │   ├── mu_denoised_copy_ratio_t.tsv
│   │   ├── mu_psi_s_log__.tsv
│   │   ├── mu_read_depth_s_log__.tsv
│   │   ├── mu_z_sg.tsv
│   │   ├── sample_name.txt
│   │   ├── std_denoised_copy_ratio_t.tsv
│   │   ├── std_psi_s_log__.tsv
│   │   ├── std_read_depth_s_log__.tsv
│   │   └── std_z_sg.tsv
│   └── SAMPLE_1
│       ├── baseline_copy_number_t.tsv
│       ├── log_c_emission_tc.tsv
│       ├── log_q_c_tc.tsv
│       ├── mu_denoised_copy_ratio_t.tsv
│       ├── mu_psi_s_log__.tsv
│       ├── mu_read_depth_s_log__.tsv
│       ├── mu_z_sg.tsv
│       ├── sample_name.txt
│       ├── std_denoised_copy_ratio_t.tsv
│       ├── std_psi_s_log__.tsv
│       ├── std_read_depth_s_log__.tsv
│       └── std_z_sg.tsv
├── CALLS_7
│   ├── calling_config.json
│   ├── denoising_config.json
│   ├── gcnvkernel_version.json
│   ├── interval_list.tsv
│   ├── SAMPLE_0
│   │   ├── baseline_copy_number_t.tsv
│   │   ├── log_c_emission_tc.tsv
│   │   ├── log_q_c_tc.tsv
│   │   ├── mu_denoised_copy_ratio_t.tsv
│   │   ├── mu_psi_s_log__.tsv
│   │   ├── mu_read_depth_s_log__.tsv
│   │   ├── mu_z_sg.tsv
│   │   ├── sample_name.txt
│   │   ├── std_denoised_copy_ratio_t.tsv
│   │   ├── std_psi_s_log__.tsv
│   │   ├── std_read_depth_s_log__.tsv
│   │   └── std_z_sg.tsv
│   └── SAMPLE_1
│       ├── baseline_copy_number_t.tsv
│       ├── log_c_emission_tc.tsv
│       ├── log_q_c_tc.tsv
│       ├── mu_denoised_copy_ratio_t.tsv
│       ├── mu_psi_s_log__.tsv
│       ├── mu_read_depth_s_log__.tsv
│       ├── mu_z_sg.tsv
│       ├── sample_name.txt
│       ├── std_denoised_copy_ratio_t.tsv
│       ├── std_psi_s_log__.tsv
│       ├── std_read_depth_s_log__.tsv
│       └── std_z_sg.tsv
├── CALLS_8
│   ├── calling_config.json
│   ├── denoising_config.json
│   ├── gcnvkernel_version.json
│   ├── interval_list.tsv
│   ├── SAMPLE_0
│   │   ├── baseline_copy_number_t.tsv
│   │   ├── log_c_emission_tc.tsv
│   │   ├── log_q_c_tc.tsv
│   │   ├── mu_denoised_copy_ratio_t.tsv
│   │   ├── mu_psi_s_log__.tsv
│   │   ├── mu_read_depth_s_log__.tsv
│   │   ├── mu_z_sg.tsv
│   │   ├── sample_name.txt
│   │   ├── std_denoised_copy_ratio_t.tsv
│   │   ├── std_psi_s_log__.tsv
│   │   ├── std_read_depth_s_log__.tsv
│   │   └── std_z_sg.tsv
│   └── SAMPLE_1
│       ├── baseline_copy_number_t.tsv
│       ├── log_c_emission_tc.tsv
│       ├── log_q_c_tc.tsv
│       ├── mu_denoised_copy_ratio_t.tsv
│       ├── mu_psi_s_log__.tsv
│       ├── mu_read_depth_s_log__.tsv
│       ├── mu_z_sg.tsv
│       ├── sample_name.txt
│       ├── std_denoised_copy_ratio_t.tsv
│       ├── std_psi_s_log__.tsv
│       ├── std_read_depth_s_log__.tsv
│       └── std_z_sg.tsv
├── CALLS_9
│   ├── calling_config.json
│   ├── denoising_config.json
│   ├── gcnvkernel_version.json
│   ├── interval_list.tsv
│   ├── SAMPLE_0
│   │   ├── baseline_copy_number_t.tsv
│   │   ├── log_c_emission_tc.tsv
│   │   ├── log_q_c_tc.tsv
│   │   ├── mu_denoised_copy_ratio_t.tsv
│   │   ├── mu_psi_s_log__.tsv
│   │   ├── mu_read_depth_s_log__.tsv
│   │   ├── mu_z_sg.tsv
│   │   ├── sample_name.txt
│   │   ├── std_denoised_copy_ratio_t.tsv
│   │   ├── std_psi_s_log__.tsv
│   │   ├── std_read_depth_s_log__.tsv
│   │   └── std_z_sg.tsv
│   └── SAMPLE_1
│       ├── baseline_copy_number_t.tsv
│       ├── log_c_emission_tc.tsv
│       ├── log_q_c_tc.tsv
│       ├── mu_denoised_copy_ratio_t.tsv
│       ├── mu_psi_s_log__.tsv
│       ├── mu_read_depth_s_log__.tsv
│       ├── mu_z_sg.tsv
│       ├── sample_name.txt
│       ├── std_denoised_copy_ratio_t.tsv
│       ├── std_psi_s_log__.tsv
│       ├── std_read_depth_s_log__.tsv
│       └── std_z_sg.tsv
├── calls_and_model_args.txt
├── docker_cid
├── genotyped-intervals-HG00096.vcf.gz
├── genotyped-segments-HG00096.vcf.gz
├── MODEL_0
│   ├── calling_config.json
│   ├── denoising_config.json
│   ├── gcnvkernel_version.json
│   ├── interval_list.tsv
│   ├── log_q_tau_tk.tsv
│   ├── mu_log_mean_bias_t.tsv
│   ├── mu_psi_t_log__.tsv
│   ├── std_log_mean_bias_t.tsv
│   └── std_psi_t_log__.tsv
├── MODEL_1
│   ├── calling_config.json
│   ├── denoising_config.json
│   ├── gcnvkernel_version.json
│   ├── interval_list.tsv
│   ├── log_q_tau_tk.tsv
│   ├── mu_log_mean_bias_t.tsv
│   ├── mu_psi_t_log__.tsv
│   ├── std_log_mean_bias_t.tsv
│   └── std_psi_t_log__.tsv
├── MODEL_10
│   ├── calling_config.json
│   ├── denoising_config.json
│   ├── gcnvkernel_version.json
│   ├── interval_list.tsv
│   ├── log_q_tau_tk.tsv
│   ├── mu_log_mean_bias_t.tsv
│   ├── mu_psi_t_log__.tsv
│   ├── std_log_mean_bias_t.tsv
│   └── std_psi_t_log__.tsv
├── MODEL_11
│   ├── calling_config.json
│   ├── denoising_config.json
│   ├── gcnvkernel_version.json
│   ├── interval_list.tsv
│   ├── log_q_tau_tk.tsv
│   ├── mu_log_mean_bias_t.tsv
│   ├── mu_psi_t_log__.tsv
│   ├── std_log_mean_bias_t.tsv
│   └── std_psi_t_log__.tsv
├── MODEL_12
│   ├── calling_config.json
│   ├── denoising_config.json
│   ├── gcnvkernel_version.json
│   ├── interval_list.tsv
│   ├── log_q_tau_tk.tsv
│   ├── mu_log_mean_bias_t.tsv
│   ├── mu_psi_t_log__.tsv
│   ├── std_log_mean_bias_t.tsv
│   └── std_psi_t_log__.tsv
├── MODEL_2
│   ├── calling_config.json
│   ├── denoising_config.json
│   ├── gcnvkernel_version.json
│   ├── interval_list.tsv
│   ├── log_q_tau_tk.tsv
│   ├── mu_log_mean_bias_t.tsv
│   ├── mu_psi_t_log__.tsv
│   ├── std_log_mean_bias_t.tsv
│   └── std_psi_t_log__.tsv
├── MODEL_3
│   ├── calling_config.json
│   ├── denoising_config.json
│   ├── gcnvkernel_version.json
│   ├── interval_list.tsv
│   ├── log_q_tau_tk.tsv
│   ├── mu_log_mean_bias_t.tsv
│   ├── mu_psi_t_log__.tsv
│   ├── std_log_mean_bias_t.tsv
│   └── std_psi_t_log__.tsv
├── MODEL_4
│   ├── calling_config.json
│   ├── denoising_config.json
│   ├── gcnvkernel_version.json
│   ├── interval_list.tsv
│   ├── log_q_tau_tk.tsv
│   ├── mu_log_mean_bias_t.tsv
│   ├── mu_psi_t_log__.tsv
│   ├── std_log_mean_bias_t.tsv
│   └── std_psi_t_log__.tsv
├── MODEL_5
│   ├── calling_config.json
│   ├── denoising_config.json
│   ├── gcnvkernel_version.json
│   ├── interval_list.tsv
│   ├── log_q_tau_tk.tsv
│   ├── mu_log_mean_bias_t.tsv
│   ├── mu_psi_t_log__.tsv
│   ├── std_log_mean_bias_t.tsv
│   └── std_psi_t_log__.tsv
├── MODEL_6
│   ├── calling_config.json
│   ├── denoising_config.json
│   ├── gcnvkernel_version.json
│   ├── interval_list.tsv
│   ├── log_q_tau_tk.tsv
│   ├── mu_log_mean_bias_t.tsv
│   ├── mu_psi_t_log__.tsv
│   ├── std_log_mean_bias_t.tsv
│   └── std_psi_t_log__.tsv
├── MODEL_7
│   ├── calling_config.json
│   ├── denoising_config.json
│   ├── gcnvkernel_version.json
│   ├── interval_list.tsv
│   ├── log_q_tau_tk.tsv
│   ├── mu_log_mean_bias_t.tsv
│   ├── mu_psi_t_log__.tsv
│   ├── std_log_mean_bias_t.tsv
│   └── std_psi_t_log__.tsv
├── MODEL_8
│   ├── calling_config.json
│   ├── denoising_config.json
│   ├── gcnvkernel_version.json
│   ├── interval_list.tsv
│   ├── log_q_tau_tk.tsv
│   ├── mu_log_mean_bias_t.tsv
│   ├── mu_psi_t_log__.tsv
│   ├── std_log_mean_bias_t.tsv
│   └── std_psi_t_log__.tsv
├── MODEL_9
│   ├── calling_config.json
│   ├── denoising_config.json
│   ├── gcnvkernel_version.json
│   ├── interval_list.tsv
│   ├── log_q_tau_tk.tsv
│   ├── mu_log_mean_bias_t.tsv
│   ├── mu_psi_t_log__.tsv
│   ├── std_log_mean_bias_t.tsv
│   └── std_psi_t_log__.tsv
└── rc
```