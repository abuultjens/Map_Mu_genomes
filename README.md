# Map_Mu_genomes
Steps to use snippy v4.4.5 to map Mu genomes against a reference chromosome

## Clone this repository
```
# run git clone
git clone https://github.com/abuultjens/Map_Mu_genomes.git

# enter the directory
cd Map_Mu_genomes
```

## Download genomes from SRA
```
# conda install entrez-direct
conda install bioconda::entrez-direct

# command to parallel download 36 Vic Mu genomes from SRA
sh fastq-dump_parallel.sh [fofn.txt] [threads]

# example of command use
sh fastq-dump_parallel.sh 36_VIC_fofn.txt 10
```

## Map reads to reference with snippy
```
# activate your snippy v4.4.5 conda environment
conda activate [environment_name]

# command to run snippy in parallel
sh snippy_parallel.sh [fofn.txt] [threads]

# example of command
sh snippy_parallel.sh 36_VIC_fofn.txt 10
```

## Make masking bed file using reference
```
# make mask bed file from reference
snippy-core --ref JKD8049.gb --mask auto
```

## Run snippy-core and inspect core SNP alignment
```
# run snippy-core
snippy-core --prefix 36_mask_test --ref JKD8049.gb --mask core.self_mask.bed $(cat 36_VIC_fofn.txt)

# use the fa tool to check the number of SNPs in the core alignment (answer should be 117 SNPs)
fa -v 36_mask_test.aln
```

