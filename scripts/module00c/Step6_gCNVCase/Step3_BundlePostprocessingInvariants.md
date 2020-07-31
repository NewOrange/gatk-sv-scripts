### BundlePostprocessingInvariants
***
#### 作用范围:
仅一次
#### 测试样本:
+ HG00096
+ HG00097
#### 所用docker镜像：
gatksv/sv-base-mini:b3af2e3
#### 所用脚本：
测试:
```xhsell
cd /.../call-BundlePostprocessingInvariants/execution


set -euo pipefail
mkdir -p out

calls_files_tar_list=/.../call-BundlePostprocessingInvariants/executi
on/write_lines_6b19cb0734375ee888f03fa5c4dc6016.tmp
model_files_tar_list=/.../call-BundlePostprocessingInvariants/executi
on/write_lines_ee7e0e3ecd0713fcc3428c06601c076a.tmp

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
#### 生成文件
```xml
.
├── calls_files_tar_list.sorted
├── case-gcnv-postprocessing-invariants.tar.gz
├── file_pairs.sorted
├── model_files_tar_list.sorted
├── write_lines_6b19cb0734375ee888f03fa5c4dc6016.tmp
└── write_lines_ee7e0e3ecd0713fcc3428c06601c076a.tmp

```