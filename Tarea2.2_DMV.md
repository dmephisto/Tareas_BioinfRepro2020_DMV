## 4.1.3 Running process_radtags

### Chapter 3 : Demultiplexing

### <span style="color:blue"> _**Introduction**_ </span>

Now that the paired-end sequences are stitched together, we will assign each sequence to the corresponding sample, a process referred to as demultiplexing.

During library preparation, each sample was assigned a specific barcode combination, with at least 3 basepair differences between each barcode used in the library. By searching for these specific sequences, which are situated at the very beginning and very end of each sequence, we can assign each sequence to its sample. We will be using ObiTools for demultiplexing our dataset today. <span style="color:red"> **ObiTools** </span> requires an additional text file with information about the barcode sequences and primer sequences in a single line per sample separated by tabs. The forward and reverse barcode (indicated in the text file by “tags”) are separated by “:”. All forward and all reverse barcodes need to be of the same length. So, if different length barcodes were used to increase complexity in the library, you will need to use multiple files per experiment <span style="color:green"> **OR** </span> add the remaining basepairs of the barcodes with longer lengths to the beginning of the forward or reverse primer. An example file can be found below.

![image-20200122200108238](/home/dmephisto/.config/Typora/typora-user-images/image-20200122200108238.png)

<span style="color:green"> **After** </span> preparing the barcode information text files, make sure you place them in the same folder as the sequence file.

```
cd path/to/text_file
scp -r file name@boros:~/path/to/sequencing_file_folder
```

<span style="color:blue"> _**Assigning sequences to corresponding samples**_ </span>

We are now ready to call the command that will assing each sequence to its correspondig sample.

~~~
ngsfilter -t Barcode_file.txt -u Unidentified_sequences.fasta -e 1 merged.fastq > merged_assigned.fastq
~~~

+ ngsfilter: allows to demultiplex sequence data by identifying barcodes and primer sequences
+ -t: used to specify the file containing the sample description
+ -u: filename used to store the sequences unassigned to any sample
+ -e: used to specify the number of errors allowed for matching primers

If differing length barcodes, and therefore multiple barcode files, were used, we can now combine these sequencing files back together.

~~~
cat sequence_file_1.fastq sequence_file_2.fastq > merged_assigned.fastq
~~~


<span style="color:green"> **Before** </span> proceeding to the next step, it would be good to have a look at the sequence file. This command can be used any time you process the sequencing file downstream.

 `obihead –without-progress-bar -n 1 merged_assigned.fastq` 

+ obihead: similar function to the head command used earlier
+ –without-progress-bar: used to not display a progress bar when command is running
+ -n: used to specify the number of sequences you want to look at

<span style="color:red"> **To continua the protocol visit** </span> [_Bioinformatics for eDNA metabarcoding_](https://otagomohio.github.io/workshops/eDNA_Metabarcoding.html)





