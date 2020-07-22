### PESRCollection(Optional)
***
#### 前置step:
无

#### 所用docker镜像：
cwhelan/sv-pipeline:cw_3c9d26c_single_sample_annotations

#### 所用脚本：
原版：

```
    set -euo pipefail
    svtk collect-pesr \
      ~{cram} \
      ~{sample_id} \
      ~{sample_id}.split.unsorted.txt \
      ~{sample_id}.disc.unsorted.txt

    # As of 11/14/2018, svtk does not sort the split file
    tmpdir=$(mktemp -d)
    sort -k1,1V -k2,2n -T $tmpdir ~{sample_id}.split.unsorted.txt > ~{sample_id}.split.txt
    sort -k1,1V -k2,2n -T $tmpdir ~{sample_id}.disc.unsorted.txt > ~{sample_id}.disc.txt

    bgzip ~{sample_id}.disc.txt
    bgzip ~{sample_id}.split.txt
    
    tabix -f -s1 -b 2 -e 2 ~{sample_id}.disc.txt.gz
    tabix -f -s1 -b 2 -e 2 ~{sample_id}.split.txt.gz
```
测试：
```
    set -euo pipefail
    svtk collect-pesr \
      /test_data/bam/HG00096.chr22.bam \
      HG00096 \
      HG00096.chr22.split.unsorted.txt \
      HG00096.chr22.disc.unsorted.txt

    # As of 11/14/2018, svtk does not sort the split file
    tmpdir=$(mktemp -d)
    sort -k1,1V -k2,2n -T $tmpdir HG00096.chr22.split.unsorted.txt >  HG00096.chr22.split.txt
    sort -k1,1V -k2,2n -T $tmpdir HG00096.chr22.disc.unsorted.txt > HG00096.chr22.disc.txt

    bgzip HG00096.chr22.disc.txt
    bgzip HG00096.chr22.split.txt
    
    tabix -f -s1 -b 2 -e 2 HG00096.chr22.disc.txt.gz
    tabix -f -s1 -b 2 -e 2 HG00096.chr22.split.txt.gz
```
#### 所用时间
很快

#### 生成文件目录
```
step04
├── HG00096.chr22.disc.txt.gz
├── HG00096.chr22.disc.txt.gz.tbi
├── HG00096.chr22.disc.unsorted.txt
├── HG00096.chr22.split.txt.gz
├── HG00096.chr22.split.txt.gz.tbi
└── HG00096.chr22.split.unsorted.txt

0 directories, 6 files
``
```