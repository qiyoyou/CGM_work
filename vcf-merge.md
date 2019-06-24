
<H2>

## Use VCFtools to merge mutiple VCF files



### 0. Create an folder and download VCFtools 

[[VCFtools download link]](https://sourceforge.net/projects/vcftools/files/)

```
cd /tempwork173/qiyoyou/
mkdir tools
cd tools/
tar -xvf vcftools_0.1.13.tar.gz
```


### 1. Go to the decompressed folder and merge all the .vcf.gz into one .vcf file

```
cd /tempwork173/qiyoyou/tools/vcftools_0.1.13/perl/
perl vcf-merge /tempwork173/qiyoyou/Liu_WES_201903/calling/temp/*.vcf.gz >| /tempwork173/qiyoyou/Liu_WES_201903/calling/temp/Variants_all_samples.vcf
```



