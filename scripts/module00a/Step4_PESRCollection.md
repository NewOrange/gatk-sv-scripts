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
      /mnt/d/Works/genes/0629/gatk/data/fc-56ac46ea-efc4-4683-b6d5-6d95bed41c5e/CCDG_13607/Project_CCDG_13607_B01_GRM_WGS.cram.2019-02-06/Sample_HG00096/analysis/HG00096.final.cram \
      HG0096 \
      HG0096.split.unsorted.txt \
      HG0096.disc.unsorted.txt

    # As of 11/14/2018, svtk does not sort the split file
    tmpdir=$(mktemp -d)
    sort -k1,1V -k2,2n -T $tmpdir HG0096.split.unsorted.txt > HG0096.split.txt
    sort -k1,1V -k2,2n -T $tmpdir HG0096.disc.unsorted.txt > HG0096.disc.txt

    bgzip HG0096.disc.txt
    bgzip HG0096.split.txt
    
    tabix -f -s1 -b 2 -e 2 HG0096.disc.txt.gz
    tabix -f -s1 -b 2 -e 2 HG0096.split.txt.gz
```