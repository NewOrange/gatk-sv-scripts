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
cut -f2 /.../inputs/1116467038/batch
.ped > sample.list
cat /.../inputs/-318581949/cnMOPS.cnMOPS.gff /.../inputs/1034727748/cnMOPS.cnMOPS.gff /.../inputs/-1906929851/cnMOPS.cnMOPS.gff /.../inputs/-553620154/cnMOPS.cnMOPS.gff /.../inputs/799689543/cnMOPS.cnMOPS.gff /.../inputs/-2141968056/cnMOPS.cnMOPS.gff /.../inputs/-788658359/cnMOPS.cnMOPS.gff /.../inputs/564651338/cnMOPS.cnMOPS.gff /.../inputs/1917961035/cnMOPS.cnMOPS.gff /.../inputs/-1023696564/cnMOPS.cnMOPS.gff /.../inputs/1289416106/cnMOPS.cnMOPS.gff /.../inputs/-1652241493/cnMOPS.cnMOPS.gff /.../inputs/-298931796/cnMOPS.cnMOPS.gff /.../inputs/1054377901/cnMOPS.cnMOPS.gff /.../inputs/-1887279698/cnMOPS.cnMOPS.gff /.../inputs/-533970001/cnMOPS.cnMOPS.gff /.../inputs/819339696/cnMOPS.cnMOPS.gff /.../inputs/-2122317903/cnMOPS.cnMOPS.gff /.../inputs/-769008206/cnMOPS.cnMOPS.gff /.../inputs/584301491/cnMOPS.cnMOPS.gff /.../inputs/292343753/cnMOPS.cnMOPS.gff /.../inputs/1645653450/cnMOPS.cnMOPS.gff /.../inputs/1899176004/cnMOPS.cnMOPS.gff /.../inputs/-1042481595/cnMOPS.cnMOPS.gff /.../inputs/310828102/cnMOPS.cnMOPS.gff /.../inputs/1664137799/cnMOPS.cnMOPS.gff /.../inputs/-1277519800/cnMOPS.cnMOPS.gff /.../inputs/75789897/cnMOPS.cnMOPS.gff /.../inputs/1429099594/cnMOPS.cnMOPS.gff /.../inputs/-1512558005/cnMOPS.cnMOPS.gff /.../inputs/-159248308/cnMOPS.cnMOPS.gff /.../inputs/1194061389/cnMOPS.cnMOPS.gff /.../inputs/1320435913/cnMOPS.cnMOPS.gff /.../inputs/-1621221686/cnMOPS.cnMOPS.
gff /.../inputs/-267911989/cnMOPS.cnMOPS.gff /.../inputs/1085397708/cnMOPS.cnMOPS.gff /.../inputs/-1856259891/cnMOPS.cnMOPS.gff /.../inputs/-502950194/cnMOPS.cnMOPS.gff /.../inputs/850359503/cnMOPS.cnMOPS.gff /.../inputs/-2091298096/cnMOPS.cnMOPS.gff /.../inputs/-737988399/cnMOPS.cnMOPS.gff /.../inputs/615321298/cnMOPS.cnMOPS.gff /.../inputs/323363560/cnMOPS.cnMOPS.gff /.../inputs/1676673257/cnMOPS.cnMOPS.gff /.../inputs/1350723561/cnMOPS.cnMOPS.gff /.../inputs/-1590934038/cnMOPS.cnMOPS.gff /.../inputs/-726485782/cnMOPS.cnMOPS.gff /.../inputs/626823915/cnMOPS.cnMOPS.gff /.../inputs/1764177270/cnMOPS.cnMOPS.gff /.../inputs/-1177480329/cnMOPS.cnMOPS.gff > cnmops.gff

mkdir calls
grep -v "#" cnmops.gff > cnmops.gff1
echo "./cnmops.gff1">GFF.list
/opt/WGD/bin/cleancnMOPS.sh -z -o calls/ -S /7703-411a-a772-33ff29fdbeee/call
-CleanCNMops/inputs/745429519/GRCh38_Nmask.bed sample.list GFF.list

zcat calls/*/*.cnMOPS.DEL.bed.gz > DELS.bed
awk -v batch=ref_panel_1kg_v1_2tong_DEL_ 'BEGIN{OFS="\t"} {print $1,$2,$3,batch,$4,"cnmops"}' DELS.bed | cat -n |\
awk 'BEGIN{OFS="\t"} {print $2,$3,$4,$5$1,$6,"DEL",$7}' | sort -k1,1V -k2,2n > ref_panel_1kg_v1_2tong.DEL.bed

cat <(echo -e "#chr\tstart\tend\tname\tsample\tsvtype\tsources") ref_panel_1kg_v1_2tong.DEL.bed  > ref_panel_1kg_v1_2tong.DEL.header.bed

zcat calls/*/*.cnMOPS.DUP.bed.gz > DUPS.bed
awk -v batch=ref_panel_1kg_v1_2tong_DUP_ 'BEGIN{OFS="\t"} {print $1,$2,$3,batch,$4,"cnmops"}' DUPS.bed | cat -n |\
awk 'BEGIN{OFS="\t"} {print $2,$3,$4,$5$1,$6,"DUP",$7}' | sort -k1,1V -k2,2n > ref_panel_1kg_v1_2tong.DUP.bed

cat <(echo -e "#chr\tstart\tend\tname\tsample\tsvtype\tsources") ref_panel_1kg_v1_2tong.DUP.bed  > ref_panel_1kg_v1_2tong.DUP.header.bed

if false; then
  mv ref_panel_1kg_v1_2tong.DUP.header.bed ref_panel_1kg_v1_2tong.DUP.header.prestitch.bed
  mv ref_panel_1kg_v1_2tong.DEL.header.bed ref_panel_1kg_v1_2tong.DEL.header.prestitch.bed
  cat /.../inputs/745429519/autosome.fai /.../inputs/745429519/allosome.fai > contig.fai
  svtk rdtest2vcf --contigs contig.fai ref_panel_1kg_v1_2tong.DUP.header.prestitch.bed sample.list dup.vcf.gz
  svtk rdtest2vcf --contigs contig.fai ref_panel_1kg_v1_2tong.DEL.header.prestitch.bed sample.list del.vcf.gz
  bash /opt/sv-pipeline/04_variant_resolution/scripts/stitch_fragmented_CNVs.sh -d dup.vcf.gz dup1.vcf.gz
  bash /opt/sv-pipeline/04_variant_resolution/scripts/stitch_fragmented_CNVs.sh -d del.vcf.gz del1.vcf.gz
  svtk vcf2bed dup1.vcf.gz dup1.bed
  cat <(echo -e "#chr\tstart\tend\tname\tsample\tsvtype\tsources") \
      <(awk -v OFS="\t" -v minsize=1000000 '{if($3-$2>minsize)print $1,$2,$3,$4,$6,$5,"cnmops_large"}' dup1.bed) >ref_panel_1kg_v1_2tong.DUP.header.bed
  svtk vcf2bed del1.vcf.gz del1.bed
  cat <(echo -e "#chr\tstart\tend\tname\tsample\tsvtype\tsources") \
      <(awk -v OFS="\t" -v minsize=1000000 '{if($3-$2>minsize)print $1,$2,$3,$4,$6,$5,"cnmops_large"}' del1.bed) >ref_panel_1kg_v1_2tong.DEL.header.bed
fi
bgzip -f ref_panel_1kg_v1_2tong.DEL.header.bed
tabix -f ref_panel_1kg_v1_2tong.DEL.header.bed.gz

bgzip -f ref_panel_1kg_v1_2tong.DUP.header.bed
tabix -f ref_panel_1kg_v1_2tong.DUP.header.bed.gz
```

#### 生成目录
所在目录：/home/user/zhangtong/gatksv_run/cromwell-executions/Module00c/c473d627-53ec-45c1-a1c2-e3d4256e0f6c/call-CNMOPS/CNMOPS/3f079fc5-7703-411a-a772-33ff29fdbeee/call-CleanCNMops/execution
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
├── DELS.bed
├── docker_cid
├── DUPS.bed
├── GFF.list
├── rc
├── ref_panel_1kg_v1_2tong.DEL.bed
├── ref_panel_1kg_v1_2tong.DEL.header.bed.gz
├── ref_panel_1kg_v1_2tong.DEL.header.bed.gz.tbi
├── ref_panel_1kg_v1_2tong.DUP.bed
├── ref_panel_1kg_v1_2tong.DUP.header.bed.gz
├── ref_panel_1kg_v1_2tong.DUP.header.bed.gz.tbi
├── sample.list
├── script
├── script.background
├── script.submit
├── stderr
├── stderr.background
├── stdout
└── stdout.background

3 directories, 25 files
```
#### 生成文件
```
ref_panel_1kg_v1_2tong.DEL.bed
ref_panel_1kg_v1_2tong.DEL.header.bed.gz
ref_panel_1kg_v1_2tong.DEL.header.bed.gz.tbi
ref_panel_1kg_v1_2tong.DUP.bed
ref_panel_1kg_v1_2tong.DUP.header.bed.gz
ref_panel_1kg_v1_2tong.DUP.header.bed.gz.tbi
```