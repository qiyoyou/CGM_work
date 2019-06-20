
<H2>

## Calculate mean coverage over exome region 

When we perform variant calling via VarScan, there is a tuning parameter (min coverage) shold be pre-specified before calling process. To select a reasonable value, we can check the mean coverage of DNA-seq data after alignment and duplicate removal.

Picard tool is available to calculate mean coverage and below is a simple example to demonstrate the workflow.

### 0. Install Picard tool in 'DNA' environment
[[link to Anaconda cloud]](https://anaconda.org/bioconda/picard)
```
conda activate DNA
conda install -c bioconda picard
```

### 1. Create a sequence dictionary for a reference sequence

Detail: [[CreateSequenceDictionary]](https://software.broadinstitute.org/gatk/documentation/tooldocs/4.0.6.0/picard_sam_CreateSequenceDictionary.php)

Activate 'DNA' environment where Picard was installed within. The reference file is 'Homo_sapiens_assembly38.fasta' and output file is named 'reference.dict'. 
```
conda activate DNA

picard CreateSequenceDictionary \
       R=/tempwork173/qiyoyou/db/grch38_bwa/Homo_sapiens_assembly38.fasta \
       O=/tempwork173/qiyoyou/Liu_WES_201903/align/reference.dict
```


### 2. Convert a BED file to a Picard Interval List

Detail: [[BedToIntervalList]](https://software.broadinstitute.org/gatk/documentation/tooldocs/4.0.0.0/picard_util_BedToIntervalList.php)

Input 'Exome-Agilent_V5.bed' and output file is named 'list.interval_list'. 'reference.dict' is the output from step 1.
```
picard BedToIntervalList \
       I=/tempwork173/qiyoyou/Liu_WES_201903/align/Exome-Agilent_V5.bed \
       O=/tempwork173/qiyoyou/Liu_WES_201903/align/list.interval_list \
       SD=/tempwork173/qiyoyou/Liu_WES_201903/align/reference.dict
```

### 3. Collect metrics about coverage and performance of whole genome sequencing (WGS) experiments

Detail: [[CollectWgsMetrics]](https://software.broadinstitute.org/gatk/documentation/tooldocs/current/picard_analysis_CollectWgsMetrics.php#--INTERVALS)

Use the script ['sk_mean_coverage'](https://github.com/qiyoyou/CGM_work/blob/master/sk_mean_coverage) to calculate coverage information for each BAM file (after alignment and duplicate removal) via [snakemake](https://snakemake.readthedocs.io/en/stable/) which is a tool of workflow management system.

```
snakemake -j 10 -s sk_mean_coverage   ## -j: number of threads used;  -s: the script to run
```
Otherwise, do this process on each BAM file. 'list.interval_list' is the output from step 2.
```
picard CollectWgsMetrics \
       I=/tempwork173/qiyoyou/Liu_WES_201903/align/input.bam \
       O=/tempwork173/qiyoyou/Liu_WES_201903/align/temp/output.bam \
       R=/tempwork173/qiyoyou/db/grch38_bwa/Homo_sapiens_assembly38.fasta \
       INTERVALS=/tempwork173/qiyoyou/Liu_WES_201903/align/list.interval_list
```


### Supplementary

Here is a old post about calculation of average coverage for a bam file. There might be another method or tools to do. 
[[Question: Tools To Calculate Average Coverage For A Bam File?]](https://www.biostars.org/p/5165/)


