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

If you are in `qc/` let's get back to the above directory to see both the raw data and the qc folder. You can go up one folder by using ```..``` meaning the above directory in the path.

```
cd ..
pwd
```

Let's make a directory for our data clean data without adapters. Removing adapters is known as `trimming adapters`

```
mkdir trimmed
```

We'll use the [Cutadapt](https://cutadapt.readthedocs.io/) software to remove adapters.

```
module spider cutadapt
module load cutadapt
```

you can access the help of cutadapt using as well as pretty much any other piece of software by using the ``help`` parameter:

```
cutadapt --help
```

The [online help](https://cutadapt.readthedocs.io/) is also excellent. 

Let's trim one file first to see if we are able to remove the adapter before doing this on all the files at once.  We'll remove the adapter as well as low quality read (i.e. quality below 20) and reads that are shorter than 50bp after adapter trimming

```
cutadapt -a CTGCAAGATCGGAAGAGC -q 20 -m 50  raw_data/WK-01.fastq.gz  -o trimmed/WK-01.fastq
```

It looks like it is trimming things based on the output. How can we know if it really worked?

## 3. Check that the adapter is removed.

Let's have a look at the generated output using fastqc and see if those adapters are gone.

```
mkdir trimmed/qc
fastqc trimmed/WK-01.fastq -o trimmed/qc
```

Navigate to your `trimmed` folder using the file explorer and have a look at the adapter content of this new FastQC html file. If you are not sure on how to get there, you can click on any folder in the path of that exploring bar at the top left (see below) to get back to your desired folder. You can also click on the small directory icon to get back all the way to the root and navigate your way back into trimmed.

![](img/Explorer_path.png)



## 4. Remove the adapters from all of the files at once.

To remove the adapter from each of the 8 files, we'll have to apply the cutadapt command above to each of the 8 files. Luckily for us, repeating things is what computers do best.  We'll learn to repeat an action using a loop.

The general structure of a loop is as below:

```
for thing in list_of_things
  do
  something to $thing
done
```
That list of things could contain thousands of objects but in our case it is just 8 files.


Let's start with an abstract example. In the example below, for each fruit in a list of fruits, we'll apply the command echo which will print the content of the variable it is applied to.
 
``` 
for  fruit in banana lemon orange
  do 
  echo $fruit
done
```

The loop repeat the code between do and done assigning the variable `$fruit` to each element one by one. The first time it runs `$fruit` is `banana`, the second time it is `lemon`, the third time it is `orange`.

the name of the variable is up to you. You could `animal` or `jdsnkfn` car if you wanted to. 


``` 
for  animal in banana lemon orange
  do 
  echo $animal
done
```

The computer does not care but make sure it make sense to you.

Let's get back to our adapters, we want to apply the cutadapt command to remove adapters to each of the 8 files at once:

```
cd raw_data/
for file in *
  do
  echo  $file
  cutadapt  -a CTGCAAGATCGGAAGAGC -q 20 -m 50   $file  -o ../trimmed/$file.trimmed.fq
done
```  

Using the \*, we are applying the loop to all the files in the folder.

let's check if we have some output using ls to visualise the content of the 'trimmed' folder


```
ls ../trimmed/
```

Well done!

Final Challenge: Use what we learnt in the first part of this lesson to quality control all of these new files.

[Link to Useful Resources](resources.md)

[Back to the homepage](index.md)


