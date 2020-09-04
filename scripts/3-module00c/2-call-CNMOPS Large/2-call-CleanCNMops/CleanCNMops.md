### CleanCNMops
***
#### 前置step:
+ Module00c.CNMOPS.GetPed
+ Module00c.CNMOPS.NormalR1
+ Module00c.CNMOPS.NormalR2
+ Module00c.CNMOPS.MaleR1
+ Module00c.CNMOPS.MaleR2
+ Module00c.CNMOPS.FemaleR1
+ Module00c.CNMOPS.FemaleR2
#### 作用范围：
仅一次
#### 测试样本:
+ HG00096
+ HG00129
#### 所用docker镜像：
+ ibio01:5000/cwhelan/sv-pipeline:cw_3c9d26c_single_sample_annotations
#### 所用脚本：

Tips： gff文件来源于：

+ NormalR1.gff
+ NormalR2.gff
+ MaleR1.gff
+ MaleR2.gff
+ FemaleR1.gff
+ FemaleR2.gff

```xhsell
set -euo pipefail
cut -f2 /.../inputs/-1126800092
/batch.ped > sample.list
cat /.../inputs/-1725629175/cnMOPS.cnMOPS.gff /.../inputs/-372319478/cnMOPS.cnMOPS.gff /.../inputs/980990219/cnMOPS.cnMOPS.gff /.../inputs/-1960667380/cnMOPS.cnMOPS.gff /.../inputs/-607357683/cnMOPS.cnMOPS.gff /.../inputs/745952014/cnMOPS.cnMOPS.gff /.../inputs/2099261711/cnMOPS.cnMOPS.gff /.../inputs/-842395888/cnMOPS.cnMOPS.gff /.../inputs/510913809/cnMOPS.cnMOPS.gff /.../inputs/1864223506/cnMOPS.cnMOPS.gff /.../inputs/1973934757/cnMOPS.cnMOPS.gff /.../inputs/-967722842/cnMOPS.cnMOPS.gff /.../inputs/385586855/cnMOPS.cnMOPS.gff /.../inputs/1738896552/cnMOPS.cnMOPS.gff /.../inputs/-1202761047/cnMOPS.cnMOPS.gff /.../inputs/150548650/cnMOPS.cnMOPS.gff /
.../inputs/1503858347/cnMOPS.cnMOPS.gff /.../inputs/-1437799252/cnMOPS.cnMOPS.gff /.../inputs/-84489555/cnMOPS.cnMOPS.gff /.../inputs/-376447293/cnMOPS.cnMOPS.gff /.../inputs/976862404/cnMOPS.cnMOPS.gff /.../inputs/492128778/cnMOPS.cnMOPS.gff /.../inputs/1845438475/cnMOPS.cnMOPS.gff /.../inputs/-1096219124/cnMOPS.cnMOPS.gff /.../inputs/257090573/cnMOPS.cnMOPS.gff /.../inputs/1610400270/cnMOPS.cnMOPS.gff /.../inputs/-1331257329/cnMOPS.cnMOPS.gff /.../inputs/22052368/cnMOPS.cnMOPS.gff /.../inputs/1375362065/cnMOPS.cnMOPS.gff /.../inputs/-1566295534/cnMOPS.cnMOPS.gff /.../inputs/-212985837/cnMOPS.cnMOPS.gff /.../inputs/651644867/cnMOPS.cnMOPS.gff /.../inputs/2004954564/cnMOPS.cnMOPS.gff /.../inputs/-936703035/cnMOPS.cnMOPS.gff /.../inputs/416606662/cnMOPS.cnMOPS.gff /.../inputs/1769916359/cnMOPS.cnMOPS.gff /.../inputs/-1171741240/cnMOPS.cnMOPS.gff /..../inputs/181568457/cnMOPS.cnMOPS.gff /.../inputs/1534878154/cnMOPS.cnMOPS.gff /.../inputs/-1406779445/cnMOPS.cnMOPS.gff /.../inputs/-53469748/cnMOPS.cnMOPS.gff /.../inputs/-345427486/cnMOPS.cnMOPS.gff /.../inputs/1007882211/cnMOPS.cnMOPS.gff /.../inputs/-930067665/cnMOPS.cnMOPS.gff /.../inputs/423242032/cnMOPS.cnMOPS.gff /.../inputs/1287690288/cnMOPS.cnMOPS.gff /.../inputs/-1653967311/cnMOPS.cnMOPS.gff /.../inputs/-317029060/cnMOPS.cnMOPS.gff /.../inputs/1036280637/cnMOPS.cnMOPS.gff > cnmops.gff

mkdir calls
grep -v "#" cnmops.gff > cnmops.gff1
echo "./cnmops.gff1">GFF.list
/opt/WGD/bin/cleancnMOPS.sh -z -o calls/ -S /cromwell-executions/Module00c/c473d627-53ec-45c1-a1c2-e3d4256e0f6c/call-CNMOPSLarge/CNMOPS/bcff0cd0-072e-40c5-80b2-e4b2decbeb12
/call-CleanCNMops/inputs/745429519/GRCh38_Nmask.bed sample.list GFF.list

zcat calls/*/*.cnMOPS.DEL.bed.gz > DELS.bed
awk -v batch=ref_panel_1kg_v1_2tong_DEL_ 'BEGIN{OFS="\t"} {print $1,$2,$3,batch,$4,"cnmops"}' DELS.bed | cat -n |\
awk 'BEGIN{OFS="\t"} {print $2,$3,$4,$5$1,$6,"DEL",$7}' | sort -k1,1V -k2,2n > ref_panel_1kg_v1_2tong.DEL.bed

cat <(echo -e "#chr\tstart\tend\tname\tsample\tsvtype\tsources") ref_panel_1kg_v1_2tong.DEL.bed  > ref_panel_1kg_v1_2tong.DEL.large.bed

zcat calls/*/*.cnMOPS.DUP.bed.gz > DUPS.bed
awk -v batch=ref_panel_1kg_v1_2tong_DUP_ 'BEGIN{OFS="\t"} {print $1,$2,$3,batch,$4,"cnmops"}' DUPS.bed | cat -n |\
awk 'BEGIN{OFS="\t"} {print $2,$3,$4,$5$1,$6,"DUP",$7}' | sort -k1,1V -k2,2n > ref_panel_1kg_v1_2tong.DUP.bed

cat <(echo -e "#chr\tstart\tend\tname\tsample\tsvtype\tsources") ref_panel_1kg_v1_2tong.DUP.bed  > ref_panel_1kg_v1_2tong.DUP.large.bed

if true; then
  mv ref_panel_1kg_v1_2tong.DUP.large.bed ref_panel_1kg_v1_2tong.DUP.large.prestitch.bed
  mv ref_panel_1kg_v1_2tong.DEL.large.bed ref_panel_1kg_v1_2tong.DEL.large.prestitch.bed
  cat /cromwell-executions/Module00c/c473d627-53ec-45c1-a1c2-e3d4256e0f6c/call-CNMOPSLarge/CNMOPS/bcff0cd0-072e-40c5-80b2-e4b2decbeb12/call-CleanCNMops/inputs/745429519/aut
osome.fai /cromwell-executions/Module00c/c473d627-53ec-45c1-a1c2-e3d4256e0f6c/call-CNMOPSLarge/CNMOPS/bcff0cd0-072e-40c5-80b2-e4b2decbeb12/call-CleanCNMops/inputs/745429519
/allosome.fai > contig.fai
  svtk rdtest2vcf --contigs contig.fai ref_panel_1kg_v1_2tong.DUP.large.prestitch.bed sample.list dup.vcf.gz
  svtk rdtest2vcf --contigs contig.fai ref_panel_1kg_v1_2tong.DEL.large.prestitch.bed sample.list del.vcf.gz
  bash /opt/sv-pipeline/04_variant_resolution/scripts/stitch_fragmented_CNVs.sh -d dup.vcf.gz dup1.vcf.gz
  bash /opt/sv-pipeline/04_variant_resolution/scripts/stitch_fragmented_CNVs.sh -d del.vcf.gz del1.vcf.gz
  svtk vcf2bed dup1.vcf.gz dup1.bed
  cat <(echo -e "#chr\tstart\tend\tname\tsample\tsvtype\tsources") \
      <(awk -v OFS="\t" -v minsize=1000000 '{if($3-$2>minsize)print $1,$2,$3,$4,$6,$5,"cnmops_large"}' dup1.bed) >ref_panel_1kg_v1_2tong.DUP.large.bed
  svtk vcf2bed del1.vcf.gz del1.bed
  cat <(echo -e "#chr\tstart\tend\tname\tsample\tsvtype\tsources") \
      <(awk -v OFS="\t" -v minsize=1000000 '{if($3-$2>minsize)print $1,$2,$3,$4,$6,$5,"cnmops_large"}' del1.bed) >ref_panel_1kg_v1_2tong.DEL.large.bed
fi
bgzip -f ref_panel_1kg_v1_2tong.DEL.large.bed
tabix -f ref_panel_1kg_v1_2tong.DEL.large.bed.gz

bgzip -f ref_panel_1kg_v1_2tong.DUP.large.bed
tabix -f ref_panel_1kg_v1_2tong.DUP.large.bed.gz
```

#### 生成目录
所在目录：/home/user/zhangtong/gatksv_run/cromwell-executions/Module00c/c473d627-53ec-45c1-a1c2-e3d4256e0f6c/call-CNMOPSLarge/CNMOPS/bcff0cd0-072e-40c5-80b2-e4b2decbeb12/call-CleanCNMops/execution
```xml
.
├── calls
│   ├── HG00096
│   │   ├── HG00096.cnMOPS.DEL.bed.gz
│   │   └── HG00096.cnMOPS.DUP.bed.gz
│   └── HG00129
│       ├── HG00129.cnMOPS.DEL.bed.gz
│       └── HG00129.cnMOPS.DUP.bed.gz
├── cnmops.gff
├── cnmops.gff1
├── contig.fai
├── del1.bed
├── del1.vcf.gz
├── DELS.bed
├── del.vcf.gz
├── del.vcf.gz.tbi
├── docker_cid
├── dup1.bed
├── dup1.vcf.gz
├── DUPS.bed
├── dup.vcf.gz
├── dup.vcf.gz.tbi
├── GFF.list
├── rc
├── ref_panel_1kg_v1_2tong.DEL.bed
├── ref_panel_1kg_v1_2tong.DEL.large.bed.gz
├── ref_panel_1kg_v1_2tong.DEL.large.bed.gz.tbi
├── ref_panel_1kg_v1_2tong.DEL.large.prestitch.bed
├── ref_panel_1kg_v1_2tong.DUP.bed
├── ref_panel_1kg_v1_2tong.DUP.large.bed.gz
├── ref_panel_1kg_v1_2tong.DUP.large.bed.gz.tbi
├── ref_panel_1kg_v1_2tong.DUP.large.prestitch.bed
├── sample.list
├── script
├── script.background
├── script.submit
├── stderr
├── stderr.background
├── stdout
└── stdout.background
```
#### 生成文件
```
ref_panel_1kg_v1_2tong.DEL.bed
ref_panel_1kg_v1_2tong.DEL.large.bed.gz
ref_panel_1kg_v1_2tong.DEL.large.bed.gz.tbi
ref_panel_1kg_v1_2tong.DEL.large.prestitch.bed
ref_panel_1kg_v1_2tong.DUP.bed
ref_panel_1kg_v1_2tong.DUP.large.bed.gz
ref_panel_1kg_v1_2tong.DUP.large.bed.gz.tbi
ref_panel_1kg_v1_2tong.DUP.large.prestitch.bed
```