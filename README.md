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

The non-interactive network downloader.
 GNU Wget is a free utility for non-interactive download of files from the Web.

## Explore the filesystem
return working directory name
```
pwd
```  
 The pwd utility writes the absolute pathname of the current working directory to the standard output.
:question: _What directory are you working in?_  

list directory contents
```
ls
```
For each operand that names a file of a type other than directory, ls displays its name as well as any requested,
     associated information.  For each operand that names a file of type directory, ls displays the names of files contained
     within that directory, as well as any requested, associated information.

     If no operands are given, the contents of the current directory are displayed.  If more than one operand is given, non-
     directory operands are displayed first; directory and non-directory operands are sorted separately and in
     lexicographical order.
:question: _What files are present?_  
```
ls -lh
```  
> [!NOTE]
> **-l**<br/>List files in the long format. <br/>The following information is displayed for each file: file mode, number of links, owner name, group name, number of bytes in the file, abbreviated month, day-of-month file was last modified, hour file last modified, minute file last modified, and the pathname. <br/>If the file or directory has extended attributes, the permissions field printed by the -l option is followed by a '@' character. <br/>Otherwise, if the file or directory has extended security information (such as an access control list), the permissions field printed by the -l option is followed by a '+' character.

> [!NOTE]
> **-h**<br/>When used with the -l option, use unit suffixes: Byte, Kilobyte, Megabyte, Gigabyte, Terabyte and Petabyte in order to reduce the number of digits to four or fewer using base 2 for sizes.

:question: _What are the file sizes?_  

## Decompress read files  
```
gunzip utk-b1-0000_1.trimP.fastq.gz utk-b1-0000_2.trimP.fastq.gz
```
compression/decompression tool

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
display first lines of a file
This filter displays the first count lines or bytes of each of the specified files, or of the standard input if no files
     are specified.  If count is omitted it defaults to 10.
:question: _How many lines per read?_  
:question: _Which line contains sequence?_  
:question: _Which line contains quality information?_  

### Count reads
```
grep "^@" utk-b1-0000_1.trimP.fastq | wc -l
```  
file pattern searcher
 The grep utility searches any given input files, selecting lines that match one or more patterns. 
word, line, character, and byte count  
The wc utility displays the number of lines, words, and bytes contained in each input file, or standard input (if no
     file is specified) to the standard output.
     -l      The number of lines in each input file is written to the standard output.
or  
```
wc -l utk-b1-0000_1.trimP.fastq
```  
then divide that number by 4 
> [!TIP]
> 4 lines = 1 read

:question: How many reads are present?

## Read QC
### Install FastQC
```
sudo apt update
```
execute a command as another user
sudo allows a permitted user to execute a command as the superuser or another user, as specified by the security
       policy.

```
sudo apt install fastqc
```
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
> [!NOTE]
> We are already starting with trimmed fastq files, so we will skip this step.

## Genome Assembly
:question: "How do reads become a genome?"
```
spades.py -1 reads_R1.fastq -2 reads_R2.fastq -o assembly
```

### Explore FASTA file
```
head contigs.fasta
```
:question: What is a contig?

### Count Contigs
```
grep ">" contigs.fasta | wc -l
```
```
grep "^>" assembly.fasta | wc -l
```
```
grep -c ">" contigs.fasta
```
### Identify Largest Contigs
```
awk '/^>/ {if(seqlen){print seqlen}; seqlen=0; next} {seqlen+=length($0)} END {print seqlen}' assembly.fasta | sort -nr | head
```
pattern-directed scanning and processing language
 Awk scans each input file for lines that match any of a set of patterns specified literally in prog or in one or more
       files specified as -f progfile.  With each pattern there can be an associated action that will be performed when a
       line of a file matches the pattern.  Each line is matched against the pattern portion of every pattern-action
       statement; the associated action is performed for each matched pattern.

sort or merge records (lines) of text and binary files
The sort utility sorts text and binary files by lines.

## Assembly QC
```
quast assembly/contigs.fasta
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





```
w
``` 
