
<H2>
  
### Overview
  
DNA-seq：

0. create an environment for DNA

   install trimmomatic, bwa, samtools and snakemake
    
1. use trimming script

    $ vim sk_trim # to revise the script
    
    $ snakemake -j 8 -s sk_trim



<H2>

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
```

