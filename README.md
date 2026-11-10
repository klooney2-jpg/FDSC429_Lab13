# FDSC429_Lab13

## Download read files

```
wget "URL"
```  

| Isolate | Groups | URLs |
| -------- | -------- | -------- |
| utk-b1-0175  | 1, 5, 8  | https://github.com/lhudson08/FDSC429_Lab13/releases/download/v1.0/utk-b1-0175_1.trimP.fastq.gz  |
| utk-b1-0204  | 3, 6, 11  | https://github.com/lhudson08/FDSC429_Lab13/releases/download/v1.0/utk-b1-0204_1.trimP.fastq.gz  |
| utk-b1-0175  | 4, 7, 12  | https://github.com/lhudson08/FDSC429_Lab13/releases/download/v1.0/utk-b1-0234_1.trimP.fastq.gz  |

utk-b1-0175:  
https://github.com/lhudson08/FDSC429_Lab13/releases/download/v1.0/utk-b1-0175_1.trimP.fastq.gz  
https://github.com/lhudson08/FDSC429_Lab13/releases/download/v1.0/utk-b1-0175_2.trimP.fastq.gz  

utk-b1-0204:  
https://github.com/lhudson08/FDSC429_Lab13/releases/download/v1.0/utk-b1-0204_1.trimP.fastq.gz  
https://github.com/lhudson08/FDSC429_Lab13/releases/download/v1.0/utk-b1-0204_2.trimP.fastq.gz  

utk-b1-0234:  
https://github.com/lhudson08/FDSC429_Lab13/releases/download/v1.0/utk-b1-0234_1.trimP.fastq.gz  
https://github.com/lhudson08/FDSC429_Lab13/releases/download/v1.0/utk-b1-0234_2.trimP.fastq.gz  


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

## Explore FASTQ reads

```
head utk-b1-0000_1.trimP.fastq
```  

_How many lines per read?_  
_Which line contains sequence?_  
_Which line contains quality information?_  

## Count reads

```
grep "^@" utk-b1-0000_1.trimP.fastq | wc -l
```  

or  

```
wc -l utk-b1-0000_1.trimP.fastq
```  
then divide that number by 4 (Remember: 4 lines = 1 read)
