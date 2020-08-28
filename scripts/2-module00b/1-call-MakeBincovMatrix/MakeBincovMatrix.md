### MakeBincovMatrix
***
#### 前置step:
Module 00a.2-call-CollectCounts

#### 所用docker镜像：
ibio01:5000/gatksv/sv-base-mini:b3af2e3

#### 测试脚本：
测试：
```shell
set -eu

# make the CollectReadCounts output consistent with the old bincov code
# determine what format this is
firstchar=$(gunzip -c /.../HG00096.counts.tsv.gz | head -c 1)
set -o pipefail
if [ $firstchar == '@' ]; then
  shift=1  # GATK CollectReadCounts (to convert from 1-based closed intervals)
else
  shift=0  # bincov sample or matrix
fi

# kill the dictionary | kill the header | adjust to bed format: 0-based half-open intervals
zcat /.../HG00096.counts.tsv.gz \
  | sed '/^@/d' \
  | sed '/^CONTIG       START   END     COUNT$/d' \
  | sed '/^#/d' \
  | awk -v x="${shift}" 'BEGIN{OFS="\t"}{$2=$2-x; print $1,$2,$3}' > locs

# determine bin size, and drop all bins not exactly equal to this size
if true; then
  sed -n '1,1000p' locs | awk '{ print $3-$2 }' \
  | sort | uniq -c | sort -nrk1,1 \
  | sed -n '1p' | awk '{ print $2 }' \
  > most_common_binsize.txt
  binsize=$( cat most_common_binsize.txt )
else
  binsize=
fi
awk -v FS="\t" -v b=$binsize '{ if ($3-$2==b) print $0 }' locs > locs2
mv locs2 locs

mkdir cargo
fileNo=0
for fil in /.../HG00129.counts.tsv.gz
do
  set +o pipefail
  firstchar=$(gunzip -c $fil | head -c 1)
  set -o pipefail
  if [ $firstchar == '@' ]; then
    shift=1
  else
    shift=0
  fi
  zcat $fil \
    | sed '/^@/d' \
    | sed '/^CONTIG     START   END     COUNT$/d' \
    | sed '/^#/d' \
    | awk -v x="${shift}" -v b=$binsize \
      'BEGIN{OFS="\t"}{$2=$2-x; if ($3-$2==b) print $0}' > fil.bincov.bed
  if ! cut -f1-3 fil.bincov.bed | cmp locs; then
    echo $fil has different intervals than /.../HG00096.counts.tsv.gz
    exit 1
  fi
  cut -f4- fil.bincov.bed > cargo/`printf "%08d" $fileNo`
  ((++fileNo))
done

echo "#Chr      Start   End     HG00096 HG00129" > ref_panel_1kg_v1_2tong.bincov.bed
paste locs cargo/* >> ref_panel_1kg_v1_2tong.bincov.bed
bgzip ref_panel_1kg_v1_2tong.bincov.bed
tabix ref_panel_1kg_v1_2tong.bincov.bed.gz
```

#### 测试目录

所在目录：/home/user/zhangtong/gatksv_run/cromwell-executions/GATKSVPipelineBatch/c76f7770-cc74-4e71-a5fd-bdbf97b16bc3/call-Module00b/Module00b/8ec11479-4a39-4d1f-ab41-61c8d2a96f11/call-MakeBincovMatrix/execution

```xml
.
├── cargo
│   ├── 00000000
│   └── 00000001
├── docker_cid
├── fil.bincov.bed
├── locs
├── most_common_binsize.txt
├── rc
├── ref_panel_1kg_v1_2tong.bincov.bed.gz
├── ref_panel_1kg_v1_2tong.bincov.bed.gz.tbi
├── script
├── script.background
├── script.submit
├── stderr
├── stderr.background
├── stdout
└── stdout.background

1 directory, 16 files
```
#### 生成文件
```
ref_panel_1kg_v1_2tong.bincov.bed.gz
ref_panel_1kg_v1_2tong.bincov.bed.gz.tbi
```