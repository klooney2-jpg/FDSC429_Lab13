# FDSC429_Lab13

## Download read files

`wget "URL"`  

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

What directory are you working in?  
`pwd`  

What files are present?  
`ls`

What are the file sizes?  
`ls -lh`

## uncompress read files  
`gunzip filename.gz`  

## Explore FASTQ reads

`head filename_R1.fastq`

How many lines per read?  
Which line contains sequence?  
Which line contains quality information?  

## Count reads

`grep "^@" unknown_isolate_R1.fastq | wc -l`

Remember: 4 lines = 1 read
