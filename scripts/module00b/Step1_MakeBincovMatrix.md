### MakeBincovMatrix
***
#### 前置step:
Module 00a.Step2

#### 所用docker镜像：
Todo

#### 所用脚本：
测试：
```shell
cd /cromwell-executions/Module00b/8c27f4b2-ef29-44de-8ff1-0b3759a09e8e/call-MakeBincovMatrix/execution

set -eu

# make the CollectReadCounts output consistent with the old bincov code
# determine what format this is
firstchar=$(gunzip -c /cromwell-executions/Module00b/8c27f4b2-ef29-44de-8ff1-0b3759a09e8e/call-MakeBincovMatrix/inputs/1502637668/HG00096.counts.tsv.gz
| head -c 1)
set -o pipefail
if [ $firstchar == '@' ]; then
  shift=1  # GATK CollectReadCounts (to convert from 1-based closed intervals)
else
  shift=0  # bincov sample or matrix
fi

# kill the dictionary | kill the header | adjust to bed format: 0-based half-open intervals
zcat /cromwell-executions/Module00b/8c27f4b2-ef29-44de-8ff1-0b3759a09e8e/call-MakeBincovMatrix/inputs/1502637668/HG00096.counts.tsv.gz \
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
for fil in /cromwell-executions/Module00b/8c27f4b2-ef29-44de-8ff1-0b3759a09e8e/call-MakeBincovMatrix/inputs/1502637668/HG00096.counts.tsv.gz
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
    echo $fil has different intervals than /cromwell-executions/Module00b/8c27f4b2-ef29-44de-8ff1-0b3759a09e8e/call-MakeBincovMatrix/inputs/1502637668/H
G00096.counts.tsv.gz
    exit 1
  fi
  cut -f4- fil.bincov.bed > cargo/`printf "%08d" $fileNo`
  ((++fileNo))
done

echo "#Chr      Start   End     HG00096" > test_hg00096.bincov.bed
paste locs cargo/* >> test_hg00096.bincov.bed
bgzip test_hg00096.bincov.bed
tabix test_hg00096.bincov.bed.gz
```

#### 生成结果
```xml
.
├── cargo
│   └── 00000000
├── docker_cid
├── fil.bincov.bed
├── locs
├── most_common_binsize.txt
├── rc
├── script
├── script.background
├── script.submit
├── stderr
├── stderr.background
├── stdout
├── stdout.background
├── test_hg00096.bincov.bed.gz
└── test_hg00096.bincov.bed.gz.tbi

1 directory, 15 files
```