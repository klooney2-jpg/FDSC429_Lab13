# FDSC429_Lab13

## Download read files
```
wget "URL"
```  
| Isolate | Grp | URLs |
| -------- | -------- | -------- |
| utk-b1-0175 | 1<br/>5<br/>8 | https://github.com/lhudson08/FDSC429_Lab13/releases/download/v1.0/utk-b1-0175_1.trimP.fastq.gz<br/>https://github.com/lhudson08/FDSC429_Lab13/releases/download/v1.0/utk-b1-0175_2.trimP.fastq.gz |
| utk-b1-0204 | 3<br/>6<br/>11 | https://github.com/lhudson08/FDSC429_Lab13/releases/download/v1.0/utk-b1-0204_1.trimP.fastq.gz<br/>https://github.com/lhudson08/FDSC429_Lab13/releases/download/v1.0/utk-b1-0204_2.trimP.fastq.gz |
| utk-b1-0175 | 4<br/>7<br/>12 | https://github.com/lhudson08/FDSC429_Lab13/releases/download/v1.0/utk-b1-0234_1.trimP.fastq.gz<br/>https://github.com/lhudson08/FDSC429_Lab13/releases/download/v1.0/utk-b1-0234_2.trimP.fastq.gz |

> [!NOTE]
> **wget**<br/>
> The non-interactive network downloader.<br/>
> Utility for non-interactive download of files from the Web.

## Explore the filesystem
### return working directory name
```
pwd
```  
> [!NOTE]
> **pwd**<br/>
> Writes the absolute pathname of the current working directory to the standard output.
:question: _What directory are you working in?_  

### list directory contents
```
ls
```

```
ls -lh
```

> [!NOTE]
> **ls**<br/>
> For each operand that names a file of a type other than directory: displays its name as well as any requested, associated information.<br/>
> For each operand that names a file of type directory: displays the names of files contained within that directory, as well as any requested, associated information.<br/>
> If no operands are given, the contents of the current directory are displayed.<br/>
> If more than one operand is given, non-directory operands are displayed first; directory and non-directory operands are sorted separately and in lexicographical order.<br/>
**-l**<br/>
> List files in the long format.<br/>
> The following information is displayed for each file: file mode, number of links, owner name, group name, number of bytes in the file, abbreviated month, day-of-month file was last modified, hour file last modified, minute file last modified, and the pathname.<br/>
> If the file or directory has extended attributes, the permissions field printed by the -l option is followed by a '@' character.<br/>
> Otherwise, if the file or directory has extended security information (such as an access control list), the permissions field printed by the -l option is followed by a '+' character.<br/>
**-h**<br/>
> When used with the -l option, use unit suffixes: Byte, Kilobyte, Megabyte, Gigabyte, Terabyte and Petabyte in order to reduce the number of digits to four or fewer using base 2 for sizes.

:question: _What files are present?_  
:question: _What are the file sizes?_  

## Decompress read files  
```
gunzip utk-b1-0000_1.trimP.fastq.gz utk-b1-0000_2.trimP.fastq.gz
```
> [!NOTE]
> **gunzip**<br/>
> compression/decompression tool

:question: _What are the file sizes after decompressing?_  
```
ls -lh
```

## FASTQ files
:question: "What are sequencing reads?"  
:question: What does a FASTQ record look like?

### Explore FASTQ file
```
head utk-b1-0000_1.trimP.fastq
```
> [!NOTE]
> **head**<br/>
> display first lines of a file
> displays the first count lines or bytes of each of the specified files, or of the standard input if no files are specified.<br/>
> If count is omitted it defaults to 10.

:question: _How many lines per read?_  
:question: _Which line contains sequence?_  
:question: _Which line contains quality information?_  

### Count reads
```
grep "^@" utk-b1-0000_1.trimP.fastq | wc -l
```  
OR  
```
wc -l utk-b1-0000_1.trimP.fastq
```  
then divide that number by 4 
> [!TIP]
> 4 lines = 1 read

> [!NOTE]
> **grep**<br/>
> file pattern searcher<br/>
> searches any given input files, selecting lines that match one or more patterns.

> [!NOTE]
> **wc**<br/>
> word, line, character, and byte count<br/>
> displays the number of lines, words, and bytes contained in each input file, or standard input (if no file is specified) to the standard output.
> **-l**
> The number of lines in each input file is written to the standard output.

:question: How many reads are present?

## Read QC
### Install FastQC
```
sudo apt update
```
```
sudo apt install fastqc
```

> [!NOTE]
> **sudo**<br/>
> execute a command as another user<br/>
> allows a permitted user to execute a command as the superuser or another user, as specified by the security policy.

### Check FastQC Installation & See Help Info
```
fastqc -h
``` 
### Run FastQC
```
fastqc utk-b1-0175_1.trimP.fastq utk-b1-0175_2.trimP.fastq 
```
For each input fastq file, it should output:
- 1 zip file
- 1 html file
In the Explorer, right click the utk-b1-0175_1.trimP_fastqc.html file, then :point_right: "Download".
Open the downloaded file.

:question: How many reads?  
:question: Average quality?  
:question: Adapter contamination?  
:question: Are the reads high quality?  

## Trim Reads
> [!IMPORTANT]
> We are already starting with trimmed fastq files, so we will skip this step.

## Genome Assembly
:question: "How do reads become a genome assembly?"
```
spades.py --isolate --only-assembler --phred-offset 33 -1 utk-b1-0000_1.trimP.fastq.gz -2 utk-b1-0000_2.trimP.fastq.gz -o assembly
```

### Explore FASTA file
```
head utk-b1-0175_contigs.fasta
```
:question: What is a contig?

### Count Contigs
```
grep "^>" utk-b1-0175_contigs.fasta | wc -l
```
### Identify Largest Contigs
```
awk '/^>/ {if(seqlen){print seqlen}; seqlen=0; next} {seqlen+=length($0)} END {print seqlen}' utk-b1-0175_contigs.fasta | sort -nr | head
```
> [!NOTE]
> **awk**<br/>
> pattern-directed scanning and processing language<br/>
> scans each input file for lines that match any of a set of patterns specified literally in prog or in one or more files specified as -f progfile.<br/>
> With each pattern there can be an associated action that will be performed when a line of a file matches the pattern.<br/>
> Each line is matched against the pattern portion of every pattern-action statement; the associated action is performed for each matched pattern.

> [!NOTE]
> **sort**<br/>
> sort or merge records (lines) of text and binary files<br/>
> sorts text and binary files by lines.

### extract the first (largest) SPAdes contig into its own FASTA file
```
awk 'BEGIN{p=0}/^>/{if(p) exit; p=1}p' utk-b1-0175_contigs.fasta > largest_contig.fasta
```

## Assembly QC
```
quast utk-b1-0175_contigs.fasta
```
:question: How many contigs are in this assembly?  
:question: Largest contig?  
:question: N50?  
:question: Is assembly quality acceptable?  
:question: How do reads differ from contigs?  

## Identify using BLAST

### Download largest contig

### Perform BLAST search
In a browser, go to this site: https://blast.ncbi.nlm.nih.gov/Blast.cgi  
:point_right: "Nucleotide BLAST"  
Under "Enter Query Sequence", :point_right: "Choose File", and upload the largest contig file.  
At the bottom, check the box next to "Show results in a new window"  
:point_right: "BLAST"

:question: "What is the organism?"
