# Manta

## 前置step

Step1_CramtoBam

## 所用docker镜像

`gatksv/manta:8645aa`

## 所用脚本

原版：

```shell
set -Eeuo pipefail

# if a preemptible instance restarts and runWorkflow.py already
# exists, manta will throw an error
if [ -f ./runWorkflow.py ]; then
  rm ./runWorkflow.py
fi

# prepare the analysis job
/usr/local/bin/manta/bin/configManta.py \
  --bam ~{bam_or_cram_file} \
  --referenceFasta ~{reference_fasta} \
  --runDir . \
  --callRegions ~{region_bed}

# always tell manta there are 2 GiB per job, otherwise it will
# scale back the requested number of jobs, even if they won't
# need that much memory
./runWorkflow.py \
  --mode local \
  --jobs ~{num_jobs} \
  --memGb $((~{num_jobs} * 2))

# inversion conversion, then compression and index
python2 /usr/local/bin/manta/libexec/convertInversion.py \
  /usr/local/bin/samtools \
  ~{reference_fasta} \
  results/variants/diploidSV.vcf.gz \
  | bcftools reheader -s <(echo "~{sample_id}") \
  > diploidSV.vcf

bgzip -c diploidSV.vcf > ~{sample_id}.manta.vcf.gz
tabix -p vcf ~{sample_id}.manta.vcf.gz
```

测试：

### 0720a

+ [gatksv/manta | Docker Hub](https://hub.docker.com/r/gatksv/manta)

```bash
docker pull gatksv/manta:8645aa
docker run --name manta --rm -it \
-v /mnt/d/Works/genes/0629/gatk/scripts:/scripts \
-v /mnt/d/Works/genes/0629/gatk/data:/data \
gatksv/manta:8645aa

cat > /mnt/d/Works/genes/0629/gatk/scripts/step3_manta.sh << 'EOF'
set -Eeuo pipefail

# if a preemptible instance restarts and runWorkflow.py already
# exists, manta will throw an error
if [ -f ./runWorkflow.py ]; then
  rm ./runWorkflow.py
fi

# prepare the analysis job
/usr/local/bin/manta/bin/configManta.py \
  --bam /data/fc-56ac46ea-efc4-4683-b6d5-6d95bed41c5e/CCDG_13607/Project_CCDG_13607_B01_GRM_WGS.cram.2019-02-06/Sample_HG00096/analysis/HG00096.final.bam \
  --referenceFasta /data/gcp-public-data--broad-references/hg38/v0/Homo_sapiens_assembly38.fasta \
  --runDir . \
  --callRegions /data/gcp-public-data--broad-references/hg38/v0/sv-resources/resources/v1/primary_contigs_plus_mito.bed.gz

# always tell manta there are 2 GiB per job, otherwise it will
# scale back the requested number of jobs, even if they won't
# need that much memory
./runWorkflow.py \
  --mode local \
  --jobs 2 \
  --memGb 4

# inversion conversion, then compression and index
python2 /usr/local/bin/manta/libexec/convertInversion.py \
  /usr/local/bin/samtools \
  /data/gcp-public-data--broad-references/hg38/v0/Homo_sapiens_assembly38.fasta \
  results/variants/diploidSV.vcf.gz \
  | bcftools reheader -s <(echo "HG0096") \
  > diploidSV.vcf

bgzip -c diploidSV.vcf > HG0096.manta.vcf.gz
tabix -p vcf HG0096.manta.vcf.gz
EOF

# in docker
mkdir /scripts/out
bash /scripts/step3_manta.sh > /scripts/out/step3_manta.sh.0720.out 2>&1 &

## out docker
tail -f /mnt/d/Works/genes/0629/gatk/scripts/out/step3_manta.sh.0720.out
```

测试结果：

```txt
# ls -lh results/*
results/evidence:
total 0

results/stats:
total 24K
-rw-r--r-- 1 root root  511 Jul 20 08:52 alignmentStatsSummary.txt
-rw-r--r-- 1 root root 5.5K Jul 21 06:49 svCandidateGenerationStats.tsv
-rw-r--r-- 1 root root 4.7K Jul 21 06:49 svCandidateGenerationStats.xml
-rw-r--r-- 1 root root 1.6K Jul 20 11:49 svLocusGraphStats.tsv

results/variants:
total 9.4M
-rw-r--r-- 1 root root 4.2M Jul 21 06:49 candidateSV.vcf.gz
-rw-r--r-- 1 root root 572K Jul 21 06:49 candidateSV.vcf.gz.tbi
-rw-r--r-- 1 root root 3.0M Jul 21 06:49 candidateSmallIndels.vcf.gz
-rw-r--r-- 1 root root 644K Jul 21 06:49 candidateSmallIndels.vcf.gz.tbi
-rw-r--r-- 1 root root 862K Jul 21 06:49 diploidSV.vcf.gz
-rw-r--r-- 1 root root  98K Jul 21 06:49 diploidSV.vcf.gz.tbi
```

获取有chr22染色体信息的bam文件：

```shell
samtools view -b -h HG00096.final.bam chr22 > HG00096.part.bam

samtools index HG00096.part.bam
```
以切分的bam文件作为输入，运行manta
