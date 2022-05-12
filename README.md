# Slivar_VCFfiltering
Running Slivar CLI tool to query and filter group/trio VCF files

## Overview

Perform filtering of WGS trios to identify candidate gene variants. In the script provided as an example, SNVs and indels were filtered for coding variants in affected individuals that followed autosomal recessive, de novo and compound heterozygous inheritance patterns.     

### Software and versions 
bcftools/1.14   
slivar/0.2.7     

## Input files 

**HG38 Reference materials**   
Homo_sapiens_assembly38.fasta  
Homo_sapiens.GRCh38.105.gff3.gz # from Ensembl ftp site 

**VCF**   
Joint called VCF file for cohort was created using GATK's HaplotypeCaller, GenomicsBDImport, VariantQualityScoreRecalibration. The VCF had to be decomposed before running Slivar. Variant sites were annotated with bcftools csq and Ensembl's GFF3 file for Hg38. 

**pedigree**  

```
#FID  IID PID MID SEX PHENO
trio1   sample1 sample2  sample3  0       2
trio1   sample2  0       0       1       1
trio1   sample3  0       0       2       1
trio2   sample4 sample5  sample6  1       2
trio2   sample5  0       0       1       1
trio2   sample6  0       0       2       1
```

**slivar-functions.js**  
Required by Slivar to define different expressions for filtering. Downloaded from [here](https://github.com/brentp/slivar/blob/master/js/slivar-functions.js)

## Running the script 

On Usyd Artemis HPC, run as:  

`qsub run_slivar.sh`  

This script annotated the cohort VCF using the GFF3 file, and prepared it for Slivar and output two filtered VCF files. One containing all rare impactful variants that matched de novo, recessive, and comphet expressions in each trio. The other VCF contained trans compound het variants.  

Reformatted Slivar .vcfs to .tsv using `tsv_slivar.sh`. On USyd Artemis HPC, run as: `bash tsv_slivar.sh`   
