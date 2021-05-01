## Quality Control for Genomic Data

Ludovic Dutoit | May 2021

## Dataset

Today we are working with some exciting real world data. 

Dr Travis Ingram sampled common bullies (*Gobiomorphus cotidianus*) from 5 to 90 m depth in four South Island lakes to test for morphological and ecological differences associated with depth in those fishes. After identifying some consistent body shape differences associated with depth, he wondered whether those differences where associated with population structure.

PICTURE OF THE FISH

While today's workshop is not going further than Quality Control of the data, You can find the published paper [here](https://cdnsciencepub.com/doi/abs/10.1139/cjfas-2020-0015). Should you be interested, [this tutorial] would allow you to explore population structure in those fishes using a pre-processed set of over XXXX thousands genetic variants.

## Accessing genetic data

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

Fastq is the standard way of presentic raw genetic data ...

less ...
press `q` to quit.

It is obviously not very practical...

cat jjjj

This data is just a small example sample containing about 100'000 reads. At times


NeSI comes with a whole suite of pre-installed softwares. They are stored away in boxes called 
*modules* that you can access whenever you need to.

To find a module

To load a module

Some of the stuff we learnt today, cd less, pwd, the potential of HPC, logging into HPC, the dtails of the fastq format, FastQC, multiQC, loop, cutadapt.. too slow then too fast is very hard to avoid
```bash
module spider FastQC
module load FastQC
fastqc *
```
let's look at one of those files...

how do we combine this info?

```
multiqc .
```

Visualise (make sure one of the sample ) ... Put the example

Resources (maybe in the index.md) file :

some more examples of my teaching....

OtagoCarpentries 

Apply for a NESI account
