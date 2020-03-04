## Assignment 5: Annotations and RNA-seq <br>
Assignment Date: Wednesday, March 4, 2020 <br>
Due Date: Wednesday, March 11, 2020 @ 11:59pm <br>

### Assignment Overview

In this assignment, you will analyze gene expression data and learn how to make several kinds of plots in the environment of your choice. 
(We suggest Python or R.) **Make sure to show your work/code in your writeup!** As before, any questions about the assignment should be posted to 
[Piazza](https://piazza.com/jhu/spring2020/en601749/home).


#### Question 1. Gene Annotation Preliminaries [10 pts]

Download the annotation of build 38 of the human genome from here:
[ftp://ftp.ensembl.org/pub/release-87/gtf/homo_sapiens/Homo_sapiens.GRCh38.87.gtf.gz](ftp://ftp.ensembl.org/pub/release-87/gtf/homo_sapiens/Homo_sapiens.GRCh38.87.gtf.gz)

- Question 1a. How many annotated protein coding genes are on each autosome of the human genome? [Hint: Protein coding genes will have "gene" in the 3rd column, and contain the following text: gene\_biotype "protein\_coding"]

- Question 1b. What is the maximum, minimum, mean, and standard deviation of the span of protein coding genes? [Hint: use the genes identified in 1b]

- Question 1c. What is the maximum, minimum, mean, and standard deviation in the number of exons for protein coding genes? [Hint: you should separately consider each isoform for each protein coding gene]


#### Question 2. Sampling Simulation [10 pts]

A typical human cell has ~250,000 transcripts, and a typical bulk RNA-seq experiment may involve millions of cells. Consequently
in an RNAseq experiment you may start with trillions of RNA molecules, although your sequencer will only give a few million to billions of reads. 
Therefore your RNAseq experiment will be a small sampling of the full composition. We hope the sequences will be a representative
sample of the total population, but if your sample is very unlucky or biased it may not represent the true distribution. We will explore
this concept by sampling a small subset of transcripts (500 to 50000) out of a much larger set (1M) so that you can evaluate this bias.

In [data1.txt](data1.txt) with 1,000,000 lines we provide an abstraction of RNA-seq data where normalization has been performed and 
the number of times a gene name occurs corresponds to the number of transcripts in the sample.

Question 2a. Randomly sample 500 rows. Do this simulation 10 times and record the relative abundance of each of the 15 genes. Make a scatterplot the mean vs. variance of each gene (x-axis=mean of gene_i, y-axis=variance of gene_i)

Question 2b. Do the same sampling experiment but sample 5000 rows each time. Again plot the mean vs. variance.

Question 2c. Do the same sampling experiment but sample 50000 rows each time. Again plot the mean vs. variance.

Question 2d. Is the variance greater in (a), (b) or (c)? What is the relationship between mean abundance and variance? Why?


#### Question 3. Differential Expression [10 pts]

Question 3a. Using the file from question 2 (data1.txt) along with [data2.txt](data2.txt), randomly sample 500 rows from each file. 
Sample 5 times for each file (this emulates making experimental replicates) and conduct a paired t-test for 
differential expression of each of the 15 genes. Which genes are significantly differentially expressed at the 0.05 level and what is their mean fold change?

Question 3b. Make a volano plot of the data: x-axis=log2(fold change of the mean expression of gene_i); y-axis=-log_10(p_value comparing the expression of gene_i). Label all of the genes that show a statistically siginificant change

Question 3c. Now sample 5000 rows 10 times from each file, equivalent to making more replicates. Which genes are now significant at the 0.05 level and what is their mean fold change?

Question 3d. Make a volcano plot using the results from 3c (label any statistically significant genes)

Question 3e. Perform the simulations from parts a/c but sample 50000 rows each time from each file. Which genes are significant and what is their mean fold change? 

Question 3f. Make a volcano plot from 3e (label any statistically significant genes)

Question 3g. Now examine the complete files: compare the fold change in the complete files vs the different subsamples. Address replicates and the size of the random sample. If you want, you can perform additional simple simulation experiments with this data - describe what you did and how it informed your answer to this question.
