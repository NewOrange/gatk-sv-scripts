### BundlePostprocessingInvariants
***
#### 前置step:
+ Module00c.gCNVCase.GermlineCNVCallerCaseMode
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
mkdir -p out

calls_files_tar_list=/.../write_lines_43dcfda1e44b84e12658958d0a260b40.tmp
model_files_tar_list=/.../write_lines_5bf307d05c8d73675eb744554fb69867.tmp

cat $calls_files_tar_list | sort -V > calls_files_tar_list.sorted
cat $model_files_tar_list | sort -V > model_files_tar_list.sorted

paste calls_files_tar_list.sorted model_files_tar_list.sorted |\
      awk '{print (NR-1)"\t"$0}' > file_pairs.sorted
OIFS=$IFS
IFS=$'\t'
while read index calls_tar model_tar; do
    mkdir -p out/CALLS_$index
    mkdir -p out/MODEL_$index
    tar xzf $calls_tar -C out/CALLS_$index
    tar xzf $model_tar -C out/MODEL_$index
    rm $calls_tar $model_tar
done < file_pairs.sorted
IFS=$OIFS

tar c -C out . | gzip -1 > case-gcnv-postprocessing-invariants.tar.gz
rm -Rf out
```

#### 生成目录
所在目录：/home/user/zhangtong/gatksv_run/cromwell-executions/Module00c/c473d627-53ec-45c1-a1c2-e3d4256e0f6c/call-gCNVCase/CNVGermlineCaseWorkflow/1768f03f-7b99-44cd-bfb0-ba6ab0941b4c/call-BundlePostprocessingInvariants/execution
```xml
.
├── calls_files_tar_list.sorted
├── case-gcnv-postprocessing-invariants.tar.gz
├── docker_cid
├── file_pairs.sorted
├── model_files_tar_list.sorted
├── rc
├── script
├── script.background
├── script.submit
├── stderr
├── stderr.background
├── stdout
├── stdout.background
├── write_lines_43dcfda1e44b84e12658958d0a260b40.tmp
└── write_lines_5bf307d05c8d73675eb744554fb69867.tmp

0 directories, 15 files
```
#### 生成文件
```
case-gcnv-postprocessing-invariants.tar.gz
```