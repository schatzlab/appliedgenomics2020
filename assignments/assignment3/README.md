## Assignment 3: Coverage, Genome Assembly, and Variant Calling
Assignment Date: Wednesday, Feb. 12, 2020 <br>
Due Date: Wednesday, Feb. 19, 2020 @ 11:59pm <br>

Some of the tools you will need to use only run in a linux or mac environment. 
If you do not have access to a linux/mac machine, download and install a virtual 
machine or ubuntu instance following the directions here: https://github.com/schatzlab/appliedgenomics2018/blob/master/assignments/virtualbox.md

Alternatively, you might also want to try out this docker instance that has these tools preinstalled: 
[https://github.com/mschatz/wga-essentials](https://github.com/mschatz/wga-essentials)


### Question 1. Coverage simulator [10 pts]

- Q1a. How many 100bp reads are needed to sequence a 1Mbp genome to 5x coverage?

- Q1b. In the language of your choice, simulate sequencing 5x coverage of a 1Mbp genome and plot the histogram of coverage. Note you do not need to actually output the sequences of the reads, you can just randomly sample positions in the genome and record the coverage. You do not need to consider the strand of each read. The start position of each read should have a uniform random probabilty at each possible starting position (1 through 999,900). You can record the coverage in an array of 1M positions. Overlay the histogram with a Poisson distribution with lambda=5

- Q1c. Using the histogram from 1b, how much of the genome has not been sequenced (has 0x coverage). How well does this match Poisson expectations?

- Q1d. Now repeat the analysis with 15x coverage: 1. simulate the appropriate number of reads, 2. make a histogram, 3. overlay a Poisson distribution
  with lambda=15, 4. compute the number of bases with 0x coverage, and 5. evaluated how well it matches the Poisson expectation.


### Question 2. de Bruijn Graph construction [10 pts]
- Q2a. Draw (by hand or by code) the de Bruijn graph for the following reads using k=3 (assume all reads are from the forward strand, no sequencing errors, complete coverage of the genome)

```
ATTCA
ATTGA
CATTG
CTTAT
GATTG
TATTT
TCATT
TCTTA
TGATT
TTATT
TTCAT
TTCTT
TTGAT
```

- Q2b. Assume that the maximum number of occurrences of any 3-mer in the actual genome is 3 using the k-mers from Q2a. Write one possible genome sequence


- Q2c. What would it take to fully resolve the genome?


### Question 3. Small Variant Analysis [10 pts]

Download chromosome 22 from build 38 of the human genome from here:  
[http://hgdownload.cse.ucsc.edu/goldenPath/hg38/chromosomes/chr22.fa.gz](http://hgdownload.cse.ucsc.edu/goldenPath/hg38/chromosomes/chr22.fa.gz)

Download the read set from here:  
[http://schatzlab.cshl.edu/data/teaching/sample.tgz](http://schatzlab.cshl.edu/data/teaching/sample.tgz)

For this question, you may find this tutorial helpful:  
[http://clavius.bc.edu/~erik/CSHL-advanced-sequencing/freebayes-tutorial.html](http://clavius.bc.edu/~erik/CSHL-advanced-sequencing/freebayes-tutorial.html)

- 3a. Using bowtie2, how many reads align to the chr22 reference? How many reads did not align? How many aligned reads had a mate that did not align (AKA singletons)? Count each read in a pair separately.  
[Hint: Build the index using `bowtie2-build`, align reads using `bowtie2`, analyze with `samtools flagstat`.]

- 3b. How many reads are mapped to the reverse strand? Count each read in a pair separately.   
[Hint: Find out what SAM flags mean [here](https://broadinstitute.github.io/picard/explain-flags.html) and use samtools view.]

- 3c. How many high-quality (QUAL > 20) single nucleotide and indel variants does the sample have? Of the indels, how many are insertions and how many are deletions?  
[Hint:  Identify variants using `freebayes` - sort the SAM file first. Then call variants with freebayes. Filter using `bcftools filter`, and summarize using `bcftools stats`.]


### Question 4. Binomial Distribution [10 pts]

- 4a. For coverage n = 10 to 200, calculate the maximum number of minor allele reads (round down) that would make your one-sided binomial test reject the null hypothesis p=0.5 at 0.05 significance. Plot coverage on the x-axis and (number of reads)/(coverage) on the y-axis. Note this is the minimum number of reads that are necessary to believe we might have a heterozygous variant on the second haplotype rather than just mere sequencing error.

- 4b. What asymptote does the plot seem to approach? Why is this?


## Packaging

The solutions to the above questions should be submitted as a single PDF document that includes your name, email address, and 
all relevant figures (as needed). Make sure to clearly label each of the subproblems and **give the exact commands** you used for 
solving the question. Submit your solutions by uploading the PDF to [GradeScope](http://www.gradescope.com/). 

If you submit after this time, you will start to use up your late days. Remember, you are only allowed 4 late days for the entire semester!



## Resources

#### [FreeBayes](https://github.com/ekg/freebayes) - Small Variant Identification

```
conda install freebayes
freebayes -f chr22.fa sample.bam > sample.vcf
```

#### [bcftools](https://samtools.github.io/bcftools/bcftools.html) - VCF Summarry

```
conda install bcftools
bcftools filter -e "QUAL<20" sample.vcf > filtered.vcf
bcftools stats filtered.vcf > stats.txt
```

#### [Bowtie2](http://bowtie-bio.sourceforge.net/bowtie2/index.shtml) - Short read aligner

```
conda install bowtie2
bowtie2-build chr22.fa chr22
bowtie2 -x chr22 -1 sample/pair.1.fq -2 sample/pair.2.fq > sample.sam
```

While running alignments, if you get an error `Warning: Exhausted best-first chunk memory for read XXXX; skipping read` increase the command-line parameter `--chunkmbs`.

