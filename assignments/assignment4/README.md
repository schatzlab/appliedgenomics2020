## Assignment 4: Bedtools and Intro to Machine Learning
Assignment Date: Wednesday Feb 19, 2020 <br>
Due Date: Wednesday, March 4, 2020 @ 11:59pm <br>

### Assignment Overview

In this assignment, you will analyze variant data and make different visualization in the language of your choice.
(We suggest Python, R, or perhaps Excel.) **Make sure to show your work/code in your writeup!** As before, any questions about the assignment should be posted to 
[Piazza](https://piazza.com/jhu/spring2020/en601749/home).


#### Question 1. De novo mutation analysis [10 pts]

For this question, we will be focusing on the de novo variants identified in this paper:<br>
[http://www.nature.com/articles/npjgenmed201627](http://www.nature.com/articles/npjgenmed201627)

Download the de novo variant positions from here (Supplementary Table S4):<br>
[http://www.nature.com/article-assets/npg/npjgenmed/2016/npjgenmed201627/extref/npjgenmed201627-s3.xlsx](http://www.nature.com/article-assets/npg/npjgenmed/2016/npjgenmed201627/extref/npjgenmed201627-s3.xlsx)

Download the gene annotation of the human genome here: <br>
[ftp://ftp.ensembl.org/pub/release-87/gff3/homo_sapiens/Homo_sapiens.GRCh38.87.gff3.gz](ftp://ftp.ensembl.org/pub/release-87/gff3/homo_sapiens/Homo_sapiens.GRCh38.87.gff3.gz)

Download the annotation of regulatory variants from here:<br>
[ftp://ftp.ensembl.org/pub/release-87/regulation/homo_sapiens/homo_sapiens.GRCh38.Regulatory_Build.regulatory_features.20161111.gff.gz](ftp://ftp.ensembl.org/pub/release-87/regulation/homo_sapiens/homo_sapiens.GRCh38.Regulatory_Build.regulatory_features.20161111.gff.gz)

**NOTE** The variants are reported using version 37 of the reference genome, but the annotation is for version 38. Fortunately, you can 'lift-over' the variants to the coordinates on the new reference genome using several avaible tools. I recommmend the [USCS liftover tool](https://genome.ucsc.edu/cgi-bin/hgLiftOver) that can do this in batch by converting the variants into BED format. Note, some variants may not successfully lift over, especially if they become repetitive and/or missing in the new reference, so please make a note of how many variants fail liftover.

- Question 1a. How many variants are in genes? [Hint: convert xlsx to BED, then `bedtools`]

- Question 1b. How many variants are in *any* annotated regulatory regions? [Hint: `bedtools`]

- Question 1c. What type of annotated regulatory region has the most variants? [Hint: `bedtools`]

- Question 1d. Is this a statistically significant number of variants (P-value < 0.05)? [Hint: If you don't want to calculate this analytically, you can do an experiment. Try simulating the same number of variants as the original file 100 times, and see how many fall into this regulatory type. If at least this many variants fall into this feature type more than 5% of the trials, this is not statistically significant]


#### Question 2. Time Series [20 pts]

[This file](http://schatz-lab.org/teaching/exercises/rnaseq/rnaseq.1.expression/expression.txt) contains normalized expression
values for 100 genes over 10 time points. Most genes have a stable background expression level, but some special genes show increased
expression over the timecourse and some show decreased expression.

- Question 2a. Cluster the genes using an algorithm of your choice. Which genes show increasing expression and which genes show decreasing expression,
and how did you determine this? What is the background expression level (numerical value) and how did you determine this?
[Hint: K-means and hierarchical clustering are common clustering algorithms you could try.]

- Question 2b. Calculate the first two principal components of the expression matrix. Show the plot and color the points based on their cluster from part (a).
Does the PC1 axis, PC2 axis, neither, or both correspond to the clustering?

- Question 2c. Create a heatmap of the expression matrix. Order the genes by cluster, but keep the time points in numerical order.

- Question 2d. Visualize the expression data using t-SNE

- Question 2e. Using the same data, visualize the expression data using UMAP

- Question 2f. In a few sentences, compare and contrast the (1) heatmap, (2) PCA, (3) t-SNE and (4) UMAP results. Be sure to comment on understandability, relative positioning of clusters,
  runtime, and any other significant factors that you see


#### Question 3. Understanding HMMs [20 pts]

Consider this HMM describing genetic (G) and intergenic (I) sequences in a bacteria:<br>
![BacterialHMM](BacterialHMM.png)

- Question 3a. Compute the probability that this HMM emitted the sequence using the forward algorithm: `CAACATTGTCGCCATTGCTCAGGGATCTTCTGAACGCTC`.<br>
You may assume the sequence begins and ends in the intergenic state. Be sure to show the entire trellis for the calculation.

- Question 3b. Using the Viterbi algorithm, what is the most like parse of this sequence into genetic and intergenic states? Be sure to show the entire trellis including the bactracking

- Question 3c. Describe in a few sentences how you could modify the HMM to evalute the forward and reverse strands at the same time.

- Question 3d. Describe in a few sentences how you could modify the HMM to also consider a third state for "promotor". 

### Packaging

Upload a single PDF document to GradeScope.

### Resources

#### [BEDTools](http://bedtools.readthedocs.io/en/latest/) - Genome Arithmetic

Get bedtools from conda, if you haven't already.

```
conda install bedtools
```


