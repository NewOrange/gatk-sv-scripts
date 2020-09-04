### GetPed
***
#### 前置step:
+ Module00c.MakeBincovMatrix
#### 作用范围：
仅一次
#### 测试样本:
+ HG00096
+ HG00129
#### 所用docker镜像：
+ ibio01:5000/ubuntu:18.04
#### 所用脚本：
```xhsell
egrep 'HG00096|HG00129' /.../1kg_ref_panel_v1_2tong.ped > batch.ped
```

#### 生成目录
所在目录：/home/user/zhangtong/gatksv_run/cromwell-executions/Module00c/c473d627-53ec-45c1-a1c2-e3d4256e0f6c/call-CNMOPSLarge/CNMOPS/bcff0cd0-072e-40c5-80b2-e4b2decbeb12/call-GetPed/execution
```xml
.
├── batch.ped
├── docker_cid
├── rc
├── script
├── script.background
├── script.submit
├── stderr
├── stderr.background
├── stdout
└── stdout.background

0 directories, 10 files
```
#### 生成文件
```
batch.ped
```