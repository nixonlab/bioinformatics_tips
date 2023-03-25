# conda



## Enironments

General purpose environment that lets you work with common bioinformatics file types:

```
mamba create -n ngsutils\
 samtools\
 picard-slim\
 sra-tools\
 pysam\
 seqtk\
 bedtools\
 bowtie2\
 bwa\
 hisat2\
 star\
 stringtie\
 gffcompare\
 gffread\
 htseq\
 subread\
 biopython\
 numpy\
 scipy\
 minimap2
``` 

Python environment with `scanpy`, `scvelo`, `cellrank` and other single-cell packages

```
mamba create -n scvelo\
  scanpy\
  anndata\
  scipy\
  numpy\
  pandas\
  matplotlib\
  basemap\
  scikit-learn\
  umap-learn\
  seaborn\
  cellrank
```
