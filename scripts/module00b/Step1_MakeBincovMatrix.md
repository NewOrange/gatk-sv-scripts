### MakeBincovMatrix
***
#### 前置step:
Module 00a.Step2

#### 所用docker镜像：
cwhelan/sv-pipeline:cw_3c9d26c_single_sample_annotations

#### 所用脚本：
原版：
```
    set -eu

    # make the CollectReadCounts output consistent with the old bincov code
    # determine what format this is
    firstchar=$(gunzip -c ~{count_files[0]} | head -c 1)
    set -o pipefail
    if [ $firstchar == '@' ]; then
      shift=1  # GATK CollectReadCounts (to convert from 1-based closed intervals)
    else
      shift=0  # bincov sample or matrix
    fi

    # kill the dictionary | kill the header | adjust to bed format: 0-based half-open intervals
    zcat ~{all_count_files[0]} \
      | sed '/^@/d' \
      | sed '/^CONTIG	START	END	COUNT$/d' \
      | sed '/^#/d' \
      | awk -v x="${shift}" 'BEGIN{OFS="\t"}{$2=$2-x; print $1,$2,$3}' > locs

    # determine bin size, and drop all bins not exactly equal to this size
    if ~{!defined(binsize)}; then
      sed -n '1,1000p' locs | awk '{ print $3-$2 }' \
      | sort | uniq -c | sort -nrk1,1 \
      | sed -n '1p' | awk '{ print $2 }' \
      > most_common_binsize.txt
      binsize=$( cat most_common_binsize.txt )
    else
      binsize=~{binsize}
    fi
    awk -v FS="\t" -v b=$binsize '{ if ($3-$2==b) print $0 }' locs > locs2
    mv locs2 locs

    mkdir cargo
    fileNo=0
    for fil in ~{sep=' ' all_count_files}
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
        | sed '/^CONTIG	START	END	COUNT$/d' \
        | sed '/^#/d' \
        | awk -v x="${shift}" -v b=$binsize \
          'BEGIN{OFS="\t"}{$2=$2-x; if ($3-$2==b) print $0}' > fil.bincov.bed
      if ! cut -f1-3 fil.bincov.bed | cmp locs; then
        echo $fil has different intervals than ~{all_count_files[0]}
        exit 1
      fi
      cut -f4- fil.bincov.bed > cargo/`printf "%08d" $fileNo`
      ((++fileNo))
    done

    echo "#Chr	Start	End	~{sep='	' all_samples}" > ~{batch}.bincov.bed
    paste locs cargo/* >> ~{batch}.bincov.bed
    bgzip ~{batch}.bincov.bed
    tabix ~{batch}.bincov.bed.gz
```
测试：
```shell
    set -eu

    # make the CollectReadCounts output consistent with the old bincov code
    # determine what format this is
    firstchar=$(gunzip -c HG0096.counts.tsv.gz | head -c 1)
    set -o pipefail
    if [ $firstchar == '@' ]; then
      shift=1  # GATK CollectReadCounts (to convert from 1-based closed intervals)
    else
      shift=0  # bincov sample or matrix
    fi

    # kill the dictionary | kill the header | adjust to bed format: 0-based half-open intervals
    zcat HG0096.counts.tsv.gz \
      | sed '/^@/d' \
      | sed '/^CONTIG	START	END	COUNT$/d' \
      | sed '/^#/d' \
      | awk -v x="${shift}" 'BEGIN{OFS="\t"}{$2=$2-x; print $1,$2,$3}' > locs

    # determine bin size, and drop all bins not exactly equal to this size
    if ~{!defined(binsize)}; then
      sed -n '1,1000p' locs | awk '{ print $3-$2 }' \
      | sort | uniq -c | sort -nrk1,1 \
      | sed -n '1p' | awk '{ print $2 }' \
      > most_common_binsize.txt
      binsize=$( cat most_common_binsize.txt )
    else
      binsize=~{binsize}
    fi
    awk -v FS="\t" -v b=$binsize '{ if ($3-$2==b) print $0 }' locs > locs2
    mv locs2 locs

    mkdir cargo
    fileNo=0
    for fil in ~{sep=' ' all_count_files}
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
        | sed '/^CONTIG	START	END	COUNT$/d' \
        | sed '/^#/d' \
        | awk -v x="${shift}" -v b=$binsize \
          'BEGIN{OFS="\t"}{$2=$2-x; if ($3-$2==b) print $0}' > fil.bincov.bed
      if ! cut -f1-3 fil.bincov.bed | cmp locs; then
        echo $fil has different intervals than ~{all_count_files[0]}
        exit 1
      fi
      cut -f4- fil.bincov.bed > cargo/`printf "%08d" $fileNo`
      ((++fileNo))
    done

    echo "#Chr	Start	End	~{sep='	' all_samples}" > ~{batch}.bincov.bed
    paste locs cargo/* >> ~{batch}.bincov.bed
    bgzip ~{batch}.bincov.bed
    tabix ~{batch}.bincov.bed.gz
```

