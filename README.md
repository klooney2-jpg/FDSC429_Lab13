# FDSC429_Lab13

## Download read files

`wget "PASTE_RELEASE_URL_HERE"`  

utk-b1-0175:  
https://github.com/lhudson08/FDSC429_Lab13/releases/download/v1.0/utk-b1-0175_1.trimP.fastq.gz  
https://github.com/lhudson08/FDSC429_Lab13/releases/download/v1.0/utk-b1-0175_2.trimP.fastq.gz  

utk-b1-0204:  
https://github.com/lhudson08/FDSC429_Lab13/releases/download/v1.0/utk-b1-0204_1.trimP.fastq.gz  
https://github.com/lhudson08/FDSC429_Lab13/releases/download/v1.0/utk-b1-0204_2.trimP.fastq.gz  

utk-b1-0234:  
https://github.com/lhudson08/FDSC429_Lab13/releases/download/v1.0/utk-b1-0234_1.trimP.fastq.gz  
https://github.com/lhudson08/FDSC429_Lab13/releases/download/v1.0/utk-b1-0234_2.trimP.fastq.gz  

## Part 1: Explore the filesystem

What directory are you working in?  
`pwd`  

What files are present?
`ls`

What are the file sizes?  
`ls -lh`

## Part 2: Explore FASTQ reads

head unknown_isolate_R1.fastq

## Part 3: Count reads

grep "^@" unknown_isolate_R1.fastq | wc -l
