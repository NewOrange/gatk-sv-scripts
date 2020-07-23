# Delly

## 前置step

Step1_CramtoBam

## 所用docker镜像

`gatksv/delly:8645aa`

## 所用脚本

原版：

```shell
    set -Eeuo pipefail
    
    BCF="~{sample_id}.delly.~{event_type}.bcf"
    echo "Running delly on event_type=~{event_type}, output=$BCF"
    delly call \
      -t ~{event_type} \
      -g "~{reference_fasta}" \
      -x "~{blacklist_intervals_file}" \
      -o "$BCF" \
      -n \
      "~{bam_or_cram_file}"
```

## 测试：
### 命令行
```
delly call \
	-t DEL \
	-g /test_data/ref_data/hg38_v0_Homo_sapiens_assembly38.fasta \
	-x /test_data/sv-resources/resources/v1/hg38_v0_sv-resources_resources_v1_delly_human.hg38.excl.tsv \
	-o HG00096.chr22.delly.DEL.bcf \
	-n \
	/test_data/bam/HG00096.part.bam

delly call \
	-t DUP \
	-g /test_data/ref_data/hg38_v0_Homo_sapiens_assembly38.fasta \
	-x /test_data/sv-resources/resources/v1/hg38_v0_sv-resources_resources_v1_delly_human.hg38.excl.tsv \
	-o HG00096.chr22.delly.DUP.bcf \
	-n \
	/test_data/bam/HG00096.part.bam
	
delly call \
	-t INV \
	-g /test_data/ref_data/hg38_v0_Homo_sapiens_assembly38.fasta \
	-x /test_data/sv-resources/resources/v1/hg38_v0_sv-resources_resources_v1_delly_human.hg38.excl.tsv \
	-o HG00096.chr22.delly.INV.bcf \
	-n \
	/test_data/bam/HG00096.part.bam
```
日志：
```
[2020-Jul-22 10:03:47] Paired-end clustering

0%   10   20   30   40   50   60   70   80   90   100%
|----|----|----|----|----|----|----|----|----|----|
***************************************************
[W::hts_idx_load2] The index file is older than the data file: /test_data/bam/HG00096.part.bam.bai
[2020-Jul-22 10:04:12] Split-read alignment

0%   10   20   30   40   50   60   70   80   90   100%
|----|----|----|----|----|----|----|----|----|----|
***************************************************
[W::hts_idx_load2] The index file is older than the data file: /test_data/bam/HG00096.part.bam.bai
[2020-Jul-22 10:04:18] Generate REF and ALT probes

0%   10   20   30   40   50   60   70   80   90   100%
|----|----|----|----|----|----|----|----|----|----|
***************************************************
[2020-Jul-22 10:04:18] SV annotation

0%   10   20   30   40   50   60   70   80   90   100%
|----|----|----|----|----|----|----|----|----|----|
***************************************************
[2020-Jul-22 10:05:11] Genotyping

0%   10   20   30   40   50   60   70   80   90   100%
|----|----|----|----|----|----|----|----|----|----|
***************************************************
[2020-Jul-22 10:05:11] Library statistics
Sample: HG00096
RG: ID=HG00096_CGGACAAC-TCCGGATT_HCJ2HDSXX_L001,ReadSize=150,Median=430,MAD=67,UniqueDiscordantPairs=53
RG: ID=HG00096_CGGACAAC-TCCGGATT_HCJ2HDSXX_L002,ReadSize=150,Median=427,MAD=66,UniqueDiscordantPairs=58
RG: ID=HG00096_CGGACAAC-TCCGGATT_HFHJKDSXX_L002,ReadSize=150,Median=425,MAD=66,UniqueDiscordantPairs=92
RG: ID=HG00096_CGGACAAC-TCCGGATT_HCJ2HDSXX_L003,ReadSize=150,Median=429,MAD=67,UniqueDiscordantPairs=61
RG: ID=HG00096_CGGACAAC-TCCGGATT_HFH2JDSXX_L002,ReadSize=150,Median=425,MAD=66,UniqueDiscordantPairs=74
RG: ID=HG00096_CGGACAAC-TCCGGATT_HFHJKDSXX_L003,ReadSize=150,Median=421,MAD=66,UniqueDiscordantPairs=82
RG: ID=HG00096_CGGACAAC-TCCGGATT_HFH2JDSXX_L003,ReadSize=150,Median=427,MAD=67,UniqueDiscordantPairs=66
RG: ID=HG00096_CGGACAAC-TCCGGATT_HCJ2HDSXX_L004,ReadSize=150,Median=427,MAD=67,UniqueDiscordantPairs=65
RG: ID=HG00096_CGGACAAC-TCCGGATT_HFH2JDSXX_L001,ReadSize=150,Median=426,MAD=66,UniqueDiscordantPairs=84
RG: ID=HG00096_CGGACAAC-TCCGGATT_HFHJKDSXX_L004,ReadSize=150,Median=426,MAD=67,UniqueDiscordantPairs=76
RG: ID=HG00096_CGGACAAC-TCCGGATT_HFH2JDSXX_L004,ReadSize=150,Median=427,MAD=67,UniqueDiscordantPairs=73
RG: ID=HG00096_CGGACAAC-TCCGGATT_HFHJKDSXX_L001,ReadSize=150,Median=423,MAD=67,UniqueDiscordantPairs=89
```
### 生成文件
```
step05

├── HG00096.chr22.delly.DEL.bcf
├── HG00096.chr22.delly.DEL.bcf.csi
├── HG00096.chr22.delly.DUP.bcf
├── HG00096.chr22.delly.DUP.bcf.csi
├── HG00096.chr22.delly.INV.bcf
├── HG00096.chr22.delly.INV.bcf.csi

0 directories, 6 files
```
