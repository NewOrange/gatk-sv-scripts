### GetPed
***
#### 作用范围:
只进行一次
#### 测试样本:
+ HG00096
+ HG00097
#### 所用docker镜像：
ubuntu:18.04
#### 所用脚本：
测试：

```xhsell
cd /.../call-GetPed/execution

egrep 'HG00096|HG00097' /.../call-GetPed/inputs/-613506260/hg38_v0_sv-resources_ref
-panel_1KG_v1_ped_1kg_ref_panel_v1.ped > batch.ped
```
#### 生成文件
```xml
.
└── batch.ped

0 directories, 10 files
```
文件内容（可能存在问题：HG00097在bed里面没有）：
```
HG00096 HG00096 0       0       1       0
```