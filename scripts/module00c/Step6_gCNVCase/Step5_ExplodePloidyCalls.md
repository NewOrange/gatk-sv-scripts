### ExplodePloidyCalls
***
#### 作用范围:
仅一次
#### 测试样本:
+ HG00096
+ HG00097
#### 所用docker镜像：
ubuntu:18.04
#### 所用脚本：
测试:
```xhsell
cd /.../call-ExplodePloidyCalls/execution


set -euo pipefail

# Extract ploidy calls
mkdir calls
tar xzf /.../call-ExplodePloidyCalls/inputs/2136129407/case-contig-pl
oidy-calls.tar.gz -C calls/

# Archive call files by sample, renaming so they will be glob'd in order
sample_ids=(HG00096 HG00097)
for (( i=0; i<2; i++ ))
do
  sample_id=${sample_ids[$i]}
  sample_no=`printf %03d $i`
  tar -czf sample_${sample_no}.${sample_id}.contig_ploidy_calls.tar.gz -C calls/SAMPLE_${i} .
done
```
#### 生成文件
```xml
.
├── calls
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
├── glob-34f37c5febe0ba9b552a086a68bda901
│   ├── cromwell_glob_control_file
│   ├── sample_000.HG00096.contig_ploidy_calls.tar.gz
│   └── sample_001.HG00097.contig_ploidy_calls.tar.gz
├── glob-34f37c5febe0ba9b552a086a68bda901.list
├── sample_000.HG00096.contig_ploidy_calls.tar.gz
└── sample_001.HG00097.contig_ploidy_calls.tar.gz
```