## Quality Control for Genomic Data

Ludovic Dutoit | May 2021

## Dataset

Today we are working with some exciting real world data. 

[Dr Travis Ingram](https://www.otago.ac.nz/zoology/staff/ingram.html) sampled common bullies (*Gobiomorphus cotidianus*) from 5 to 90 m depth in four South Island lakes to test for morphological and ecological differences associated with depth in those fishes. After identifying some consistent body shape differences associated with depth, he wondered whether those differences reflected population structure and proceeded with genetic analyses for fishes sampled from two of those lakes (lake Wanaka and  lake Wakatipu) using a technique called [Genotyping-by-Sequencing](https://sapac.illumina.com/techniques/sequencing/dna-sequencing/targeted-resequencing/genotyping-by-sequencing.html).

 <br><img src="img/Common_bully,_Gobiomorphus_cotidianus.png" alt="drawing" size="200"/>
Picture: [Zureks](https://en.wikipedia.org/wiki/Common_bully#/media/File:Common_bully,_Gobiomorphus_cotidianus.jpg)

While today's workshop is not going further than Quality Control of the data, You can find the published paper [here](https://cdnsciencepub.com/doi/abs/10.1139/cjfas-2020-0015). Should you be interested, [this tutorial](https://github.com/ldutoit/bully_gbs/blob/master/populationstructure_tuto/populationstructure_tuto.md) will allow you to explore population structure in those fishes using a pre-processed set of 9605 genetic variants.

## Raw genetic data format

We'll first navigate to our home directory by typing:

```bash
cd 
pwd
```

we'll create a folder in which we can work for today:

```bash
mkdir tuto_insertyourname
cd tuto_insertyourname
```

If your name is Jo:

```bash
mkdir tuto_Jo
cd tuto_Jo
```

We'll then download our dataset for today and unzip it. There are other ways to get your data onto NeSI from your own computer, but a quick download will be the most efficient for us today.

```bash
wget --no-check-certificate 'https://tinyurl.com/rawingram' -O raw_data.tar
```

you can use `ls` that stands for *list* to see what is around and then decompress this `tar` archive folder. 

```bash
ls
tar xvf raw_data.tar
ls raw_data/
```


There are 8 samples, 4 from lake Wakatipu (WK)and 4 from lake Wanaka (WK)/

The [fastq format](https://en.wikipedia.org/wiki/FASTQ_format) is a standard way of storing raw genetic data.

Let's have a look at one of those files together using the command ```less```

```bash
less raw_data/WK-01.fastq.gz
```
Each read is on four lines:

* Line 1 start with a '@' character followed by a unique read identifier
* Line 2 is the sequence
* Line 3 begins with a '+' character and is sometimes by the sequence identifier (not in our case
* Line 4 encodes the quality values for the sequence in Line 2, Each base quality is encoded as one letter according to a  [translation table](). The quality score is called the PHRED score and is on a log-scale. A PHRED score of 10 means that this base has a probability of error of 10%, a score of 20: 1%, 30:0.1% and 40: 0.01%/ Another way of thinking about itis that 1 out of 10'000 bases with a score of 40 will bea sequencing error. 

press `q` to quit. 

### Quality control of individual files using FastQC

It is not very practical to look at all those reads manually, but it is always a good idea to have a very quick look at your data.

```FastQC``` is a great software to summarise `.fastq` files.

NeSI comes with a whole suite of pre-installed softwares, and [FastQC](https://www.bioinformatics.babraham.ac.uk/projects/fastqc/) is one of them. All those softwares are stored away in boxes called *modules* that you can access whenever you need to.

Loading software on the server is a case-sensitive process. We need to find the exact name under which the module is stored inside the system.

To find a module including the word *fastqc* in its name or description:

```bash
module spider fastqc
```

Now that we found it, we can load it:

```bash
module load FastQC
```
Before running the software we''ll create a `qc` folder to store cleanly our quality control files next to our raw_data folder.

```bash
cd ../
mkdir qc
```

you now hot wo go back up one folder!

mkdir fastqc


```bash
fastqc raw_data/* -o qc/
```

the star is a little *wild card* that means *everything*. In our case we run fastqc on all the files that start inside raw_data/ and store the output `-o` inside the folder qc.

Go checkout this file....

### MultiQC

[MultiQC](https://multiqc.info/) aggregates results from bioinformatics analyses across many samples into a single report. Today, we'll just aggregate our results from the fastqc analysis, but MultiQC recognises log files of many different softwares and is an excellent way of keeping track of your samples along an analysis pipeline whether.

Find and load MultiQC

```bash
module spider MultiQC
module load MultiQC
```

```bash
cd qc 
multiqc .
```

Visualise the multiqc_report.html file just produced. 

[Let's learn how to remove those adapters](remove_adapters.md)

[Back to the homepage](index.md)


