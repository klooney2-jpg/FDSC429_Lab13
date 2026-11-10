# FDSC429_Lab13

## Download read files
```
wget "URL"
```  
| Isolate | Grp | URLs |
| -------- | -------- | -------- |
| utk-b1-0175 | 1,5,8 | https://github.com/lhudson08/FDSC429_Lab13/releases/download/v1.0/utk-b1-0175_1.trimP.fastq.gz<br/>https://github.com/lhudson08/FDSC429_Lab13/releases/download/v1.0/utk-b1-0175_2.trimP.fastq.gz |
| utk-b1-0204 | 3,6,11 | https://github.com/lhudson08/FDSC429_Lab13/releases/download/v1.0/utk-b1-0204_1.trimP.fastq.gz<br/>https://github.com/lhudson08/FDSC429_Lab13/releases/download/v1.0/utk-b1-0204_2.trimP.fastq.gz |
| utk-b1-0175 | 4,7,12 | https://github.com/lhudson08/FDSC429_Lab13/releases/download/v1.0/utk-b1-0234_1.trimP.fastq.gz<br/>https://github.com/lhudson08/FDSC429_Lab13/releases/download/v1.0/utk-b1-0234_2.trimP.fastq.gz |

## Explore the filesystem
_What directory are you working in?_  
```
pwd
```  
_What files are present?_  
```
ls
```  
_What are the file sizes?_  
```
ls -lh
```  

## Decompress read files  
```
gunzip utk-b1-0000_1.trimP.fastq.gz utk-b1-0000_2.trimP.fastq.gz
```
_What are the file sizes after decompressing?_  
```
ls -lh
```  
## FASTQ files
"What are sequencing reads?"
What does a FASTQ record look like?
### Explore FASTQ file
```
head utk-b1-0000_1.trimP.fastq
```  
_How many lines per read?_  
_Which line contains sequence?_  
_Which line contains quality information?_  

### Count reads
```
grep "^@" utk-b1-0000_1.trimP.fastq | wc -l
```  
or  
```
wc -l utk-b1-0000_1.trimP.fastq
```  
then divide that number by 4 (Remember: 4 lines = 1 read)
How many reads are present?

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
In the Explorer, right click the utk-b1-0175_1.trimP_fastqc.html file, then click "Download".
Open the downloaded file.

How many reads?  
Average quality?  
Adapter contamination?  
Are the reads high quality?  

## Trim Reads
We are already starting with trimmed fastq files, so we will skip this step.

## Genome Assembly
"How do reads become a genome?"
```
spades.py -1 reads_R1.fastq -2 reads_R2.fastq -o assembly
```

### Explore FASTA file
```
head contigs.fasta
```
What is a contig?

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
How many contigs are in this assembly?  
Largest contig?  
N50?  
Is assembly quality acceptable?  
How do reads differ from contigs?  

## Identify using BLAST

### Download largest contig

### Perform BLAST search
In a browser, go to this site: https://blast.ncbi.nlm.nih.gov/Blast.cgi  
Click "Nucleotide BLAST"  
Under "Enter Query Sequence", click "Choose File", and upload the largest contig file.  
At the bottom, check the box next to "Show results in a new window"  
Click "BLAST"

"What is the organism?"





```
w
``` 
