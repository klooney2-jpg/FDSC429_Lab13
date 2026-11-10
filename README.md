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

## Explore the filesystem
return working directory name
```
pwd
```  
:question: _What directory are you working in?_  

list directory contents
```
ls
```
:question: _What files are present?_  
```
ls -lh
```  
> [!NOTE]
> -l   List files in the long format. The following information is displayed for each file: file mode, number of links, owner name, group name, number of bytes in the file, abbreviated month, day-of-month file was last modified, hour file last modified, minute file last modified, and the pathname.  If the file or directory has extended attributes, the permissions field printed by the -l option is followed by a '@' character.  Otherwise, if the file or directory has extended security information (such as an access control list), the permissions field printed by the -l option is followed by a '+' character.
> [!NOTE]
> -h   When used with the -l option, use unit suffixes: Byte, Kilobyte, Megabyte, Gigabyte, Terabyte and Petabyte in order to reduce the number of digits to four or fewer using base 2 for sizes.
:question: _What are the file sizes?_  

## Decompress read files  
```
gunzip utk-b1-0000_1.trimP.fastq.gz utk-b1-0000_2.trimP.fastq.gz
```
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
:question: _How many lines per read?_  
:question: _Which line contains sequence?_  
:question: _Which line contains quality information?_  

### Count reads
```
grep "^@" utk-b1-0000_1.trimP.fastq | wc -l
```  
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
