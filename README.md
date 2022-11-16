[(Nucleomics-VIB)](https://github.com/Nucleomics-VIB)

## Disclaimer

This newtflow pipeline was developped by the Pacbio team and not by me! I only provide here information on how to use it and some example results onbtained from our own Sequel-IIe data.

## Where to start?

Please start by reading the full information present on the source github **[pb-16S-nf](https://github.com/PacificBiosciences/pb-16S-nf)** repo.

The code should be installed from the original github.

The full list of ``pb-16S-nf nextflow`` commands for that pipeline can be obtained with the comamnd:

```
nextflow run main.nf --help

  Usage:
  This pipeline takes in the standard sample manifest and metadata file used in
  QIIME 2 and produces QC summary, taxonomy classification results and visualization.

  For samples TSV, two columns named "sample-id" and "absolute-filepath" are
  required. For metadata TSV file, at least two columns named "sample_name" and
  "condition" to separate samples into different groups.

  nextflow run main.nf --input samples.tsv --metadata metadata.tsv \\
    --dada2_cpu 8 --vsearch_cpu 8

  By default, sequences are first trimmed with cutadapt. If adapters are already trimmed, you can skip 
  cutadapt by specifying "--skip_primer_trim".

  Other important options:
  --front_p    Forward primer sequence. Default to F27. (default: AGRGTTYGATYMTGGCTCAG)
  --adapter_p    Reverse primer sequence. Default to R1492. (default: AAGTCGTAACAAGGTARCY)
  --filterQ    Filter input reads above this Q value (default: 20).
  --max_ee    DADA2 max_EE parameter. Reads with number of expected errors higher than
              this value will be discarded (default: 2)
  --minQ    DADA2 minQ parameter. Reads with any base lower than this score 
            will be removed (default: 0)
  --min_len    Minimum length of sequences to keep (default: 1000)
  --max_len    Maximum length of sequences to keep (default: 1600)
  --pooling_method    QIIME 2 pooling method for DADA2 denoise see QIIME 2 
                      documentation for more details (default: "pseudo", alternative: "independent") 
  --maxreject    max-reject parameter for VSEARCH taxonomy classification method in QIIME 2
                 (default: 100)
  --maxaccept    max-accept parameter for VSEARCH taxonomy classification method in QIIME 2
                 (default: 100)
  --min_asv_totalfreq    Total frequency of any ASV must be above this threshold
                         across all samples to be retained. Set this to 0 to disable filtering
                         (default 5)
  --min_asv_sample    ASV must exist in at least min_asv_sample to be retained. 
                      Set this to 0 to disable. (default 1)
  --vsearch_identity    Minimum identity to be considered as hit (default 0.97)
  --rarefaction_depth    Rarefaction curve "max-depth" parameter. By default the pipeline
                         automatically select a cut-off above the minimum of the denoised 
                         reads for >80% of the samples. This cut-off is stored in a file called
                         "rarefaction_depth_suggested.txt" file in the results folder
                         (default: null)
  --dada2_cpu    Number of threads for DADA2 denoising (default: 8)
  --vsearch_cpu    Number of threads for VSEARCH taxonomy classification (default: 8)
  --cutadapt_cpu    Number of threads for primer removal using cutadapt (default: 16)
  --outdir    Output directory name (default: "results")
  --vsearch_db	Location of VSEARCH database (e.g. silva-138-99-seqs.qza can be
                downloaded from QIIME database)
  --vsearch_tax    Location of VSEARCH database taxonomy (e.g. silva-138-99-tax.qza can be
                   downloaded from QIIME database)
  --silva_db   Location of Silva 138 database for taxonomy classification 
  --gtdb_db    Location of GTDB r202 for taxonomy classification
  --refseq_db    Location of RefSeq+RDP database for taxonomy classification
  --skip_primer_trim    Skip all primers trimming (switch off cutadapt and DADA2 primers
                        removal) (default: trim with cutadapt)
  --skip_nb    Skip Naive-Bayes classification (only uses VSEARCH) (default: false)
  --colorby    Columns in metadata TSV file to use for coloring the MDS plot
               in HTML report (default: condition)
  --run_picrust2    Run PICRUSt2 pipeline. Note that pathway inference with 16S using PICRUSt2
                    has not been tested systematically (default: false)
  --download_db    Download databases needed for taxonomy classification only. Will not
                   run the pipeline. Databases will be downloaded to a folder "databases"
                   in the Nextflow pipeline directory.
  --version    Output version
```

## Zymo D6305 pb-16S-nf_tutorial

Pacbio 16S data analysis using the Pacbio **pb-16S-nf** nextflow pipeline and reads from 5 *ZymoBIOMICS Microbial Community DNA Standard* samples replicates ([ref](https://www.zymoresearch.com/collections/zymobiomics-microbial-community-standards/products/zymobiomics-microbial-community-dna-standard)).

The **[Zymo_pb-16S-nf.pdf](https://github.com/Nucleomics-VIB/pb-16S-nf_tutorial/blob/main/Zymo_pb-16S-nf.pdf)** document describes installing and running the pipeline on 5 samples produced in the lab and using v0.4 of the pipeline (commit:763d542c5c82adb6cff769e253ebc15f61d765cb). It rephrases most of the content of the original repo and comments on the used tools.

The results of running the pipeline on five of our Zymo samples are also uploaded here in **[Zymo-SequelIIe-Hifi_results_local](https://github.com/Nucleomics-VIB/pb-16S-nf_tutorial/tree/main/Zymo-SequelIIe-Hifi_results_local)** for review


**Note:** the pipeline sets automatically the parameter ``--rarefaction_depth``to keep 80% of the samples and returns the obtained value in ``rarefaction_depth_suggested.txt``. When the user wants all samples retained, review of the ``alpha-rarefaction-curves.qzv``object in the **Qiime2 viewer** will allow defining a better value for that cutoff and rerun the pipeline with the addition of ``--rarefaction_depth <optimal value>`` 

**Alternatively**, you can resume the first run (avoid repeating the lengthy denoising and alignment steps) at the point of rarefaction and replace later results by running the pipeline with ``-resume --rarefaction_depth <optimal value>``

*[[back-to-top](#top)]*  

## What next?

### Interactive webtools

The pipeline produces a number of Qiime2 objects that can be converted to graphics or tables using the **[QIIME2 Viewer and integrated Emperor webtool](https://view.qiime2.org/)** or **[iTol (for trees)](https://itol.embl.de/)**.

### R integration

For more advanced follow-up analyzes, the user can use the many tools present in the **[Qiime2 package](https://qiime2.org/)** and get support from the **[Qiime2 Forum](https://forum.qiime2.org/)** as well as import the objects in R and create custom plots or downstream analyses there using the **[qiime2R R package](https://github.com/jbisanz/qiime2R)** (see **[tutorial on the qiime2 pages](https://forum.qiime2.org/t/tutorial-integrating-qiime2-and-r-for-data-visualization-and-analysis-using-qiime2r/4121)**)

```
# install the R package and dependencies with the following commands (here using Bioconductor):
if (!require("BiocManager", quietly = TRUE)){install.packages("BiocManager"); BiocManager::install(version = "3.16")}
BiocManager::install(c("ape","Biostrings","biomformat","phyloseq","Hmisc","yaml","tidyr","dplyr","stats","utils"))

if (!requireNamespace("devtools", quietly = TRUE)){install.packages("devtools")}
devtools::install_github("jbisanz/qiime2R")
```

The **qiime2R** package adds the following Functions:

```
read_qza() - Function for reading artifacts (.qza).
qza_to_phyloseq() - Imports multiple artifacts to produce a phyloseq object.
read_q2metadata() - Reads qiime2 metadata file (containing q2-types definition line)
write_q2manifest() - Writes a read manifest file to import data into qiime2
theme_q2r() - A ggplot2 theme for for clean figures.
print_provenance() - A function to display provenance information.
is_q2metadata() - A function to check if a file is a qiime2 metadata file.
parse_taxonomy() - A function to parse taxonomy strings and return a table where each column is a taxonomic class.
parse_ordination() - A function to parse the internal ordination format.
read_q2biom() - A function for reading QIIME2 biom files in format v2.1
make_clr() - Transform feature table using centered log2 ratio.
make_proportion() - Transform feature table to proportion (sum to 1).
make_percent() - Transform feature to percent (sum to 100).
interactive_table() - Create an interactive table in Rstudio viewer or rmarkdown html.
summarize_taxa()- Create a list of tables with abundances sumed to each taxonomic level.
taxa_barplot() - Create a stacked barplot using ggplot2.
taxa_heatmap() - Create a heatmap of taxonomic abundances using gplot2.
corner() - Show top corner of a large table-like object.
min_nonzero() - Find the smallest non-zero, non-NA in a numeric vector.
mean_sd() - Return mean and standard deviation for plotting.
subsample_table() - Subsample a table with or without replacement.
filter_features() - Remove low abundance features by number of counts and number of samples they appear in.
```

<hr>

<h4>Please send comments and feedback to <a href="mailto:nucleomics.bioinformatics@vib.be">nucleomics.bioinformatics@vib.be</a></h4>

<hr>

![Creative Commons License](http://i.creativecommons.org/l/by-sa/3.0/88x31.png?raw=true)

This work is licensed under a [Creative Commons Attribution-ShareAlike 3.0 Unported License](http://creativecommons.org/licenses/by-sa/3.0/).
