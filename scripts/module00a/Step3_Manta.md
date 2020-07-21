### Manta
***
#### 前置step:
Step1_CramtoBam

#### 所用docker镜像：
gatksv/manta:8645aa

#### 所用脚本：
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
```shell
    set -Eeuo pipefail
    
    # if a preemptible instance restarts and runWorkflow.py already
    # exists, manta will throw an error
    if [ -f ./runWorkflow.py ]; then
      rm ./runWorkflow.py
    fi
    
    # prepare the analysis job
    /usr/local/bin/manta/bin/configManta.py \
      --bam /mnt/d/Works/genes/0629/gatk/data/fc-56ac46ea-efc4-4683-b6d5-6d95bed41c5e/CCDG_13607/Project_CCDG_13607_B01_GRM_WGS.cram.2019-02-06/Sample_HG00096/analysis/HG00096.final.bam \
      --referenceFasta /mnt/d/Works/genes/0629/gatk/data/gcp-public-data--broad-references/hg38/v0/Homo_sapiens_assembly38.fasta \
      --runDir . \
      --callRegions /mnt/d/Works/genes/0629/gatk/data/gcp-public-data--broad-references/hg38/v0/sv-resources/resources/v1/primary_contigs_plus_mito.bed.gz
    
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
      /mnt/d/Works/genes/0629/gatk/data/gcp-public-data--broad-references/hg38/v0/Homo_sapiens_assembly38.fasta \
      results/variants/diploidSV.vcf.gz \
      | bcftools reheader -s <(echo "HG0096") \
      > diploidSV.vcf
    
    bgzip -c diploidSV.vcf > HG0096.manta.vcf.gz
    tabix -p vcf HG0096.manta.vcf.gz
```

获取有chr22,chr15染色体信息的bam文件：
```
samtools view -b -h /mnt/d/Works/genes/0629/gatk/data/fc-56ac46ea-efc4-4683-b6d5-6d95bed41c5e/CCDG_13607/Project_CCDG_13607_B01_GRM_WGS.cram.2019-02-06/Sample_HG00096/analysis/HG00096.final.bam chr15 chr22 > /mnt/d/Works/genes/0629/gatk/data/fc-56ac46ea-efc4-4683-b6d5-6d95bed41c5e/CCDG_13607/Project_CCDG_13607_B01_GRM_WGS.cram.2019-02-06/Sample_HG00096/analysis/HG00096.part.bam

samtools sort /mnt/d/Works/genes/0629/gatk/data/fc-56ac46ea-efc4-4683-b6d5-6d95bed41c5e/CCDG_13607/Project_CCDG_13607_B01_GRM_WGS.cram.2019-02-06/Sample_HG00096/analysis/HG00096.part.sort.bam

samtools index /mnt/d/Works/genes/0629/gatk/data/fc-56ac46ea-efc4-4683-b6d5-6d95bed41c5e/CCDG_13607/Project_CCDG_13607_B01_GRM_WGS.cram.2019-02-06/Sample_HG00096/analysis/HG00096.part.sort.bam
```

以切分的bam文件作为输入，运行manta