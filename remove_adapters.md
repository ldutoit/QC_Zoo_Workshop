## Remove adapters

The one thing that struck us when we looked at our data is the presence of adapters. Those are attached to the end of the sequences of interest prior to sequencing.. As we sequence short fragments, the machine start reading the adapters before stopping. We simply need to remove those adapters so that we only keep sequences of interest.

We'll proceed in 4 steps:

1. Identify our adapter sequence
2. Remove it from one file
3. Check that the adapter is removed.
4. Remove the adapters from all of the files at once.

## 1. Identify our adapter sequence

The first step in removing the adapter is knowing uts sequence. In general, you or other members of your group will probably know what your adapter is or be able to identify what the sequence is with the sequencing provider.

Our adapter sequence is: AGATCGGAAGAGC


## 2. Remove it from one file


Let's remember ourselves where we are:

```
pwd
```

let's get back to the above directory to see both the raw data and the qc folder. You can go up one folder by using ../

cd ..

mkdir trimmed



module spider cutadapt
module load cutadapt


you can access the help of cutadapt using as well as pretty much any other piece of software by using the ``help`` parameter:

```
cutadapt --help
```

Let's trim one file first to see if we are able to remove the adapter before doing this on all the files at once. 

Let's remove the adapter as well as low quality read (i.e. quality below 20) and reads that are shorter than 50bp after adapter trimming

```
cutadapt -a AGATCGGAAGAGC -q 20 -m 50  raw_data/WK-01.fastq.gz  -o trimmed/WK-01.fastq
```
It looks like it is trimming thigs based on the output. How can we know if it really worked?

## 3. Check that the adapter is removed.

```
fastqc trimmed/WK-01.fastq
```

Navigate to your folder using the file explorer

## 4. Remove the adapters from all of the files at once.

To remove the adapter from each of the 8 files, we'll have to apply the cutadapt command above to each of the 8 files. Luckily for us, repeating things is what computer do best.  We'll learn to repeat an action using a loop.

The general structure of a loop is as below:

```
for thing in list_of_things
  do
  something to $thing
  done
```

 In the example below, for each fruit in a list of fruits, we'll apply the command echo ...
 
 
for  fruit in banana lemon orange
  do 
  echo $fruit
  done

Now in our case, we have to ...

...
for file in ...
 do
  ...
  done
  
Well done!

Final Challenge: Use what we learnt in the first part of this lesson to quality control all of these new files.

lesson summary

Back to homepage



