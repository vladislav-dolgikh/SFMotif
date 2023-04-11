SFMotif
=========================

Introduction
--------------------------------------------------
A cis-regulatory code is a system of rules according to which the binding of transcription factors with cis-regulatory elements in promoter regions of genes determines their transcriptional response. The task of completely deciphering the universal cis-regulatory code is currently not resolved. Its solution is reduced to the reconstruction of single events. The key to understanding the mechanisms of cis-regulatory code functioning is the integration of genome-wide data, which makes it possible to look at its different aspects. An example of data suitable for such integration is the ChIP-seq/RNA-seq pair. ChIP-seq data, as a rule, carry information not only about the structure of the target binding motif of the studied TF, but also about alternative binding motifs (if any), and motifs of TF partners, which makes them a suitable starting point for the reconstruction of composite elements and cis. - regulatory modules. RNA-seq data make it possible to detect the coordinated transcriptional response of genes at the genome-wide level. We have developed the SFMotif pipeline (from Structure and Function analysis of Motifs) to perform this kind of analysis.

![image](https://user-images.githubusercontent.com/83860672/226091061-f0629115-ddf0-44bb-9a85-084b8b25682f.png)


Requirements
------------

### TOOLS:

- **Homer** 

Download and installation manual for **Homer** is on official website: http://homer.ucsd.edu/homer/. After installing tool you need to install ***TAIR10*** promoter set to the Homer environment. This can be done with the command:

`perl configureHomer.pl -install tair10`

The program must be in PATH. **Homer** contains executable files in the `bin` directory. For example, if homer is installed in the `/user/programs/homer/` directory, then you need to specify PATH with the command:

`PATH='/user/programs/homer/bin/:$PATH'`


- **bedtools**

Download and installation manual for **bedtools** is on official website: https://bedtools.readthedocs.io/en/latest/.

- **MCOT**

Download and installation manual for **MCOT** is on official website https://github.com/academiq/mcot-kernel/.

The program must be in PATH. **MCOT** contains necessary executable file for **anchor_vs_one_partner** subprogram in the `src/anchor_vs_one_partner` directory. For example, if **MCOT** is installed in the `/user/programs/MCOT/` directory, and your copy of program is in subdirectory called `mcot_for_sfmotif` then you need to specify PATH with the command:

`PATH='/user/programs/MCOT/mcot_for_sfmotif/src/anchor_vs_one_partner':$PATH`

### R packages

- universalmotif
- igraph
- purrr
- stringr
- ggplot2
- magrittr
- dplyr
- Biostrings

Installation of this packages in **R** is carried out using the commands

```
install.packages('universalmotif')
install.packages('igraph')
install.packages('purrr')
install.packages('stringr')
install.packages('ggplot2')
install.packages('magrittr')
install.packages('dplyr')

if (!require("BiocManager", quietly = TRUE))
    install.packages("BiocManager")
BiocManager::install("Biostrings")
```

Installation
------------

Installing a package from source is done in the R environment using the command:

`install.packages("path/to/SFMotif_0.0.0.9000.tar.gz", repos = NULL, type="source")`

Usage
------

**SFMotif** requires as input files ***ChIP-seq*** peaks in `BED` format (`BED3` is sufficient) and ***RNA-seq*** data in the form of a matrix of differentially expressed genes in the following format:

 ```
AT1G01010	NON
AT1G01030	DOWN
AT1G01040	NON
AT1G01046	NON
AT1G01050	UP
AT1G01073	NON
AT1G01080	UP
AT1G01110	NON
AT1G01100	UP
AT1G01115	NON
AT1G01130	NON
AT1G01160	NON
AT1G01150	UP
AT1G01170	NON
AT1G01183	NON
```

`NON` correspond by not differential expressed gene and `UP` and `DOWN`  correspond by up- and down-regulated genes.

**SFMotif** receives the length of the bin into which the cis-regulatory region of the gene is divided as a launch parameter. Accepts values `100`, `300` and `500`.

**SFMotif** launches with command:

`Rscript -e 'SFMotif::sfmotif_launch(peaks_file = "path/to/peaks.bed", deg_matrix = "path/to/deg_matrix.txt", bin_length = 300)'`





