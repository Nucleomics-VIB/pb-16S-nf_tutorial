[(Nucleomics-VIB)](https://github.com/Nucleomics-VIB)

## Disclaimer

This newtflow pipeline was developped by the Pacbio team and not by me! I only provide here information on how to use it and some example results onbtained from our own Sequel-IIe data.

## Where to start?

Please start by reading the full information present on the source github **[pb-16S-nf](https://github.com/PacificBiosciences/pb-16S-nf)** repo.

The code should be installed from the original github.

The full list of ``pb-16S-nf nextflow`` commands for that pipeline can be obtained with the comamnd:

```
nextflow run main.nf --help
```

## pb-16S-nf_tutorial

Pacbio 16S data analysis using the Pacbio **pb-16S-nf** nextflow pipeline and reads from 5 *ZymoBIOMICS Microbial Community DNA Standard* samples replicates ([ref](https://www.zymoresearch.com/collections/zymobiomics-microbial-community-standards/products/zymobiomics-microbial-community-dna-standard)).

The **[Zymo_pb-16S-nf.pdf](https://github.com/Nucleomics-VIB/pb-16S-nf_tutorial/blob/main/Zymo_pb-16S-nf.pdf)** document describes installing and running the pipeline on 5 samples produced in the lab and using v0.4 of the pipeline (commit:763d542c5c82adb6cff769e253ebc15f61d765cb). It rephrases most of the content of the original repo and comments on the used tools.

The results of running the pipeline on five of our Zymo samples are also uploaded here in **[Zymo-SequelIIe-Hifi_results_local](https://github.com/Nucleomics-VIB/pb-16S-nf_tutorial/tree/main/Zymo-SequelIIe-Hifi_results_local)** for revew and explorations using Qiime2 commands or the [Qiime2-viewer](https://view.qiime2.org/).

*[[back-to-top](#top)]*  

## What next?

The pipeline produces a number of Qiime2 objects that can be replayed using the **[QIIME2 Viewer and integrated Emperor webtool](https://view.qiime2.org/)** or **[iTol (for trees)](https://itol.embl.de/)**.

For more advanced follow-up analyzes, the user can use the many tools present in the Qiime2 package as well as import the objects in R and create custom plots or downstream analyses there using the **[qiime2R R package](https://github.com/jbisanz/qiime2R)** (see **[tutorial on the qiime2 pages](https://forum.qiime2.org/t/tutorial-integrating-qiime2-and-r-for-data-visualization-and-analysis-using-qiime2r/4121)**)

if (!requireNamespace("devtools", quietly = TRUE)){install.packages("devtools")}
devtools::install_github("jbisanz/qiime2R")

<hr>

<h4>Please send comments and feedback to <a href="mailto:nucleomics.bioinformatics@vib.be">nucleomics.bioinformatics@vib.be</a></h4>

<hr>

![Creative Commons License](http://i.creativecommons.org/l/by-sa/3.0/88x31.png?raw=true)

This work is licensed under a [Creative Commons Attribution-ShareAlike 3.0 Unported License](http://creativecommons.org/licenses/by-sa/3.0/).
