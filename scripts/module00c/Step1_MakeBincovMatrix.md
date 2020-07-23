### MakeBincovMatrix
***
#### 前置step:
Todo
#### 测试样本:
+ HG00096
+ HG00097
#### 所用docker镜像：
Todo
#### 所用脚本：
测试：
```xhsell
cd /.../call-MakeBincovMatrix/execution


set -eu

# make the CollectReadCounts output consistent with the old bincov code
# determine what format this is
firstchar=$(gunzip -c /cromwell-executions/GATKSVPipelinePhase1/8d210b54-725e-47f8-aa63-3c21b9aa8f31/call-Module00c/Module00c/b362
d99d-0e0b-47a8-8322-c6bd753e915f/call-MakeBincovMatrix/inputs/1502637668/HG00096.chr22.counts.tsv.gz | head -c 1)
set -o pipefail
if [ $firstchar == '@' ]; then
  shift=1  # GATK CollectReadCounts (to convert from 1-based closed intervals)
else
  shift=0  # bincov sample or matrix
fi

# kill the dictionary | kill the header | adjust to bed format: 0-based half-open intervals
zcat /cromwell-executions/GATKSVPipelinePhase1/8d210b54-725e-47f8-aa63-3c21b9aa8f31/call-Module00c/Module00c/b362d99d-0e0b-47a8-83
22-c6bd753e915f/call-MakeBincovMatrix/inputs/1502637668/HG00096.chr22.counts.tsv.gz \
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
for fil in /cromwell-executions/GATKSVPipelinePhase1/8d210b54-725e-47f8-aa63-3c21b9aa8f31/call-Module00c/Module00c/b362d99d-0e0b-4
7a8-8322-c6bd753e915f/call-MakeBincovMatrix/inputs/1502637668/HG00096.chr22.counts.tsv.gz /cromwell-executions/GATKSVPipelinePhase
1/8d210b54-725e-47f8-aa63-3c21b9aa8f31/call-Module00c/Module00c/b362d99d-0e0b-47a8-8322-c6bd753e915f/call-MakeBincovMatrix/inputs/
1502637668/HG00097.chr22.counts.tsv.gz
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
    echo $fil has different intervals than /cromwell-executions/GATKSVPipelinePhase1/8d210b54-725e-47f8-aa63-3c21b9aa8f31/call-Mod
ule00c/Module00c/b362d99d-0e0b-47a8-8322-c6bd753e915f/call-MakeBincovMatrix/inputs/1502637668/HG00096.chr22.counts.tsv.gz
    exit 1
  fi
  cut -f4- fil.bincov.bed > cargo/`printf "%08d" $fileNo`
  ((++fileNo))
done

echo "#Chr      Start   End     HG00096 HG00097" > ref_panel_v1.bincov.bed
paste locs cargo/* >> ref_panel_v1.bincov.bed
bgzip ref_panel_v1.bincov.bed
tabix ref_panel_v1.bincov.bed.gz
```
#### inputs
```xml

```

#### 生成结果
```xml
.
├── cargo
│   ├── 00000000
│   └── 00000001
├── fil.bincov.bed
├── locs
├── most_common_binsize.txt
├── rc
├── ref_panel_v1.bincov.bed.gz
└── ref_panel_v1.bincov.bed.gz.tbi
```