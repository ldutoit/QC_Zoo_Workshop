## Remove adapters

The one thing that struck us when we looked at our data, is the presence of adapters. Those are attached to the end of the sequences of interest. As we sequence short fragments, the machine start reading the adapters before stopping. We simply need to remove those adapters so that we are back to our original sequences.


We'll proceed in 4 steps:

1. Identify our adapter sequence
2. Remove it from one file
3. Check that the adapter is removed.
4. Remove the adapters from all of the files at once.

## 1. Identify our adapter sequence

The first step in removing the adapter is knowing uts sequence. In general, you or other members of your group will probably know what your adapter is or be able to identify what the sequence is with the sequencing provider.
When that is not the cas, FastQC is pretty helpful. our FastQC reports stated that the contamination came from ...

You can go to the FastQC documentation and find the exact serquence: .....

## 2. Remove it from one file

Get in the right folder

create trimming

load cutadapt

cutadapt -q 20 ... --- remove sequence that are shorter than X...


It looks like it is trimming thigs based on the output

## 3. Check that the adapter is removed.

fastqc ...

## 4. Remove the adapters from all of the files at once.

for thing in list_of_things
  do
  something to $thing
  done

for  fruit in banana lemon orange
  do 
  echo $fruit
  done


...
for file in ...
 do
  ...
  done
  
Well done!

Final Challenge: Use what we learnt in the first part of this lesson to quality control all of these new files.

lesson summary

Back to homepage



