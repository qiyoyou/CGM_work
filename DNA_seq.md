
<H2>
  
### 0. Overview
  
DNA-seq：

0. create an environment for DNA

   install trimmomatic, bwa, samtools and snakemake
    
1. use trimming script

    $ vim sk_trim # to revise the script
    
    $ snakemake -j 8 -s sk_trim



<H2>

### 1. Preparation

#### 0.1 install Miniconda3 in Linux
```
cd /tempwork173/qiyoyou/
wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh
bash Miniconda3-latest-Linux-x86_64.sh
source /home/qiyoyou/.bashrc
```

#### 0.2 create an environment
```
conda create -n py3.7 python=3.7
source activate py3.7
deactivate
```

#### 1.1 create an environment named 'DNA' and activate this environment
```
conda create -n DNA python=3.7
conda activate DNA
```

#### 1.2 install 'fastqc', 'multiqc', 'trimmomatic', 'bwa', 'samtools' and 'snakemake' in DNA enviroment
```
conda install -c bioconda fastqc
conda install -c bioconda multiqc
conda install -c bioconda trimmomatic
conda install -c bioconda bwa
conda install -c bioconda samtools
conda install -c bioconda snakemake
```

<H2>

### 2. Quality Check

#### 2.1 Make sure you activate the enviromment since we installed 'fastqc' within and change direction to the folder containing raw .fastq data
```
conda activate DNA
cd /tempwork173/qiyoyou/Liu_WES_201903/RawData/
```

#### 2.2 Quality check with 'fastqc'. Apply fastqc to all file with '.gz' pattern (It usually takes a lot of time if sequence data being large)
```
fastqc *.gz   ## 
```

#### 2.3 Quality check with 'multiqc'. Apply multiqc to the output (.html) in this folder (./). This process integrate all the seperate output .html files into one.
```
multiqc ./   ## 
```


