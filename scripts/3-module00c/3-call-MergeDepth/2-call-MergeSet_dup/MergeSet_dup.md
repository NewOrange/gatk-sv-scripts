### MergeSet_dup
***
#### 前置step:
+ Module00c.MergeDepth.MergeSample_dup
#### 作用范围：
仅一次
#### 测试样本:
+ HG00096
+ HG00129
#### 所用docker镜像：
+ ibio01:5000/gatksv/sv-base-mini:b3af2e3
#### 所用脚本：
```xhsell
set -euo pipefail

# TODO: fail fast if localization failed. This is a Cromwell issue.
while read file; do
  if [ ! -f $file ]; then
    echo "Localization failed: ${file}" >&2
    exit 1
  fi
done < /.../write_lines_0ee8e1cf0733186f6c4978dc7f441455.tmp;

zcat -f /.../HG00096.merged.defrag.sorted.bed /.../HG00129.merged.defrag.sorted.bed \
  | sort -k1,1V -k2,2n \
  | awk -v OFS="\t" -v svtype=DUP -v batch=ref_panel_1kg_v1_2tong '{$4=batch"_"svtype"_"NR; print}' \
  | cat <(echo -e "#chr\\tstart\\tend\\tname\\tsample\\tsvtype\\tsources") - \
  | bgzip -c > ref_panel_1kg_v1_2tong.DUP.bed.gz;
tabix -p bed ref_panel_1kg_v1_2tong.DUP.bed.gz
```

#### 生成目录
所在目录：/home/user/zhangtong/gatksv_run/cromwell-executions/Module00c/9689f669-dda1-40b4-a6df-aa35c9d84202/call-MergeDepth/MergeDepth/86744103-1c75-47aa-be83-cdcba8448706/call-MergeSet_dup/execution
```xml
.
├── docker_cid
├── rc
├── ref_panel_1kg_v1_2tong.DUP.bed.gz
├── ref_panel_1kg_v1_2tong.DUP.bed.gz.tbi
├── script
├── script.background
├── script.submit
├── stderr
├── stderr.background
├── stdout
├── stdout.background
└── write_lines_0ee8e1cf0733186f6c4978dc7f441455.tmp

0 directories, 12 files
```
#### 生成文件
```
ref_panel_1kg_v1_2tong.DUP.bed.gz
ref_panel_1kg_v1_2tong.DUP.bed.gz.tbi
```