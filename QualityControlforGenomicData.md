## Quality Control for Genomic Data

Ludovic Dutoit | May 2021

## Dataset

Today we are working with some exciting real world data. 

[Dr Travis Ingram](https://www.otago.ac.nz/zoology/staff/ingram.html) sampled common bullies (*Gobiomorphus cotidianus*) from 5 to 90 m depth in four South Island lakes to test for morphological and ecological differences associated with depth in those fishes. After identifying some consistent body shape differences associated with depth, he wondered whether those differences reflected population structure and proceeded with genetic analyses for fishes sampled from two of those lakes (lake Wanaka and  lake Wakatipu) using a technique called [Genotyping-by-Sequencing](https://sapac.illumina.com/techniques/sequencing/dna-sequencing/targeted-resequencing/genotyping-by-sequencing.html).

PICTURE OF THE FISH

While today's workshop is not going further than Quality Control of the data, You can find the published paper [here](https://cdnsciencepub.com/doi/abs/10.1139/cjfas-2020-0015). Should you be interested, [this tutorial](https://github.com/ldutoit/bully_gbs/blob/master/populationstructure_tuto/populationstructure_tuto.md) will allow you to explore population structure in those fishes using a pre-processed set of 9605 genetic variants.

## Raw genetic data format

We'll first navigate to our home directory by typing:

```bash
cd 
pwd
```

We'll then download our dataset for today and unzip it. There are other ways to get your data onto NeSI from your own computer, but a quick download will be the most efficient for us today.

```bash
wget ...
unzip ...
```

here are 24 samples:

Genetic data 
Open a fastq file

The [fastq format](https://en.wikipedia.org/wiki/FASTQ_format) is a standard way of storing raw genetic data.

Let's have a look at one of those files together using the command ```less```

```bash
less ....
```

Each read is on four lines:

MORE INFO
* Line 1 start with a '@' character followed by a unique read identifier
* Line 2 is the sequence
* Line 3 begins with a '+' character and is sometimes by the sequence identifier
* Line 4 encodes the quality values for the sequence in Line 2, Each base quality is encoded as one letter according to a  [translation table](). The quality score is called the PHRED score and is on a log-scale. A PHRED score of 10 means that this base has a probability of error of 10%, a score of 20, 1%. 30 0.1%, ... Another way of seeing it is that 1 out of 10'000 bases with a score of 40 will be wrong. 

press `q` to quit. 

### Quality control of individual files using FastQC

It is obviously not very practical to look at all those reads manually, but always a good idea to have a very quick look at your data.

```FastQC``` is a great software to summarise the information.


NeSI comes with a whole suite of pre-installed softwares. They are stored away in boxes called 
*modules* that you can access whenever you need to. Let's see if we can can find FastQC as one of those pre-installed softwares.

To find a module

To load a module

```bash
module spider FastQC
module load FastQC
fastqc *
```
let's look at one of those files.

....Navigate to FastQC file

....

### MultiQC...

[MultiQC](https://multiqc.info/) aggregates results from bioinformatics analyses across many samples into a single report. We'll just aggregate our results from the fastqc analysis, but MultiQC recognises log files of many different softwares and is an excellent way of keeping track of your samples along an analysis pipeline.

Find and load MultiQC

```bash
module spider multiqc
module load multiqc
```
...

```bash
multiqc .
```

Visualise (make sure one of the sample ) ... Put the example

[Let's learn how to remove those adapters](remove_adapters.md)
[Back to the homepage](index.md)


Resources (maybe in the index.md) file :

some more examples of my teaching....

OtagoCarpentries 

Apply for a NESI account

Some of the stuff we learnt today, cd less, pwd, the potential of HPC, logging into HPC, the dtails of the fastq format, FastQC, multiQC, loop, cutadapt.. too slow then too fast is very hard to avoid
The cutadapt loop
the new fastqc .
