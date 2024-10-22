DADA2 and Phyloseq Pipeline for 16S rRNA Data Analysis

This pipeline performs 16S rRNA amplicon sequencing data analysis using the DADA2 and Phyloseq R packages. It processes FASTQ files, performs quality filtering, learns error rates, dereplicates sequences, merges paired-end reads, removes chimeras, and assigns taxonomy. Finally, it creates a phyloseq object for downstream ecological analysis.

Files and Directories

FASTQ Files: Located in /mmfs1/scratch/godson.aryee/Kaffi_data, following the naming convention SampleName_1.fastq for forward reads and SampleName_2.fastq for reverse reads.
Filtered FASTQ Files: Written to the filtered/ subdirectory within the same path.
Metadata File: A tab-delimited file Metafile.txt containing metadata for all samples.
Taxonomic Training Data: The Silva 138.1 prokaryotic SSU taxonomic training data file used for assigning taxonomy: silva_nr99_v138.1_wSpecies_train_set.fa.
Output Files: CSV files and figures summarizing sequence data, taxonomy, and read counts.
Prerequisites

R Libraries
DADA2: For processing and analyzing amplicon data.
ggplot2: For generating plots.
Phyloseq: For managing and analyzing phylogenetic sequencing data.
Biostrings: For handling biological sequences.
Other packages: data.table, dplyr, reshape, magrittr, vegan
Installation
To install the required R packages, run:
install.packages(c("ggplot2", "data.table", "dplyr", "reshape", "magrittr", "vegan"))
BiocManager::install(c("dada2", "phyloseq", "Biostrings"))
Pipeline Steps

1. Quality Profile Visualization
The first step is to visualize the quality profiles of the first 10 forward reads and 20 reverse reads:

Plots are generated using plotQualityProfile() and saved as .tiff files.
2. Filtering and Trimming
The FASTQ files are filtered to remove poor-quality reads based on defined thresholds:

Parameters: Trimming length of 200 bp for both forward and reverse reads, maxEE set to 5, truncQ set to 2.
Output files are saved to the filtered/ directory.
3. Learning Error Rates
DADA2 learns the error rates from the filtered reads using learnErrors(). Plots of these error models are generated and saved.

4. Dereplication
Sequences are dereplicated (i.e., identical sequences are collapsed into a single sequence). Dereplication reduces computational load for subsequent steps.

5. Inferring Sequence Variants
The dada() function is used to infer the exact sequence variants from the dereplicated reads. These are referred to as "amplicon sequence variants" (ASVs).

6. Merging Paired-End Reads
Forward and reverse reads are merged using mergePairs(). This step joins the overlapping regions of paired reads to form full-length amplicon sequences.

7. Removing Chimeras
Chimeric sequences, which result from artifacts during amplification, are removed using removeBimeraDenovo().

8. Assigning Taxonomy
Taxonomy is assigned to the sequence variants using the Silva 138.1 reference database. The resulting taxonomy table is saved as a CSV file.

9. Phyloseq Object Construction
A phyloseq object is created using the sequence table, taxonomy table, and metadata:

ASV sequences are renamed with ASV numbers for ease of reference.
The phyloseq object is saved as ps1.rds.
10. Removal of Unwanted Taxa
Taxa belonging to Eukaryota, Chloroplasts, and Mitochondria are removed from the dataset.

11. Summarizing Read Counts
A summary of the total reads per sample is generated and saved as kaffi_third_Reads_per_sample.csv.

Output Files

Filtered FASTQ Files: Stored in the filtered/ directory.
Quality Plots: fnFs_plotQualityProfile_2.tiff, fnRs_plotQualityProfile.tiff
Error Rate Plots: Forward_error_plot.tiff, Reverse_error_plot.tiff
Sequence Table (No Chimeras): Seqsnochim_Kaffi_2024_16S.csv
Taxonomy Table: Taxa_Kaffi_2024_16S.csv
Phyloseq Object: ps1.rds
Reads per Sample: kaffi_Reads_per_sample.csv
How to Run

To run the pipeline:

Set up your working directory by changing the setwd() command at the top of the script to your data path.
Ensure that all the required files (FASTQ, metadata, taxonomic reference data) are in place.
Knit the RMarkdown document or run the R script in your R environment.
