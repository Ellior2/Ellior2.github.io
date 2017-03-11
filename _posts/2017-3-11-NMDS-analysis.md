---

layout: post
title: 2016 Data Processing-NMDS
---

03/11/2017

### NMDS in R using Vegan

I am using non-metric multidimensional (NMDS) to examine similarity between technical replicates using the vegan and raster packages in R.

First I took the Abacus_output.tsv file, imported it into Excel and removed all columns except:   

- PROTID   
- PROTLEN   
- the sample columns with addendum _ADJNSAF   

I relabeled the column headers as followed for convience:   

| sample ID | Sample # | new sample ID | Column # on CSV file | Contents                    |
|-----------|----------|---------------|----------------------|-----------------------------|
| pool0     | 1        | 60            | 2                    | pooled larvae               |
| pool0     | 1A       | 61            | 3                    | pooled larvae               |
| S2CD3     | 3        | 62            | 4                    | Silo 2, Cold, Day 3, Rep 1  |
| S2CD3     | 3A       | 63            | 5                    | Silo 2, Cold, Day 3, Rep 2  |
| S3CD3     | 4        | 64            | 6                    | Silo 3, Cold, Day 3, Rep 1  |
| S3CD3     | 4A       | 65            | 7                    | Silo 3, Cold, Day 3, Rep 2  |
| S9HD3     | 8        | 66            | 8                    | Silo 9, Hot, Day 3, Rep 1   |
| S9HD3     | 8A       | 67            | 9                    | Silo 9, Hot, Day 3, Rep 2   |
| S2CD5     | 11       | 68            | 10                   | Silo 2, Cold, Day 5, Rep 1  |
| S2CD5     | 11A      | 69            | 11                   | Silo 2, Cold, Day 5, Rep 2  |
| S3CD5     | 12       | 70            | 12                   | Silo 3, Cold, Day 5, Rep 1  |
| S3CD5     | 12A      | 71            | 13                   | Silo 3, Cold, Day 5, Rep 2  |
| S9HD5     | 16       | 72            | 14                   | Silo 9, Hot, Day 5, Rep 1   |
| S9HD5     | 16A      | 73            | 15                   | Silo 9, Hot, Day 5, Rep 2   |
| S2CD7     | 19       | 74            | 16                   | Silo 2, Cold, Day 7, Rep 1  |
| S2CD7     | 19A      | 75            | 17                   | Silo 2, Cold, Day 7, Rep 2  |
| s3CD7     | 20       | 76            | 18                   | Silo 3, Cold, Day 7, Rep 1  |
| S3CD7     | 20A      | 77            | 19                   | Silo 3, Cold, Day 7, Rep 2  |
| S9HD7     | 24       | 78            | 20                   | Silo 9, Hot, Day 7, Rep 1   |
| S9HD7     | 24A      | 79            | 21                   | Silo 9, Hot, Day 7, Rep 2   |
| S2CD9     | 27       | 80            | 22                   | Silo 2, Cold, Day 9, Rep 1  |
| S2CD9     | 27A      | 81            | 23                   | Silo 2, Cold, Day 9, Rep 2  |
| S3CD9     | 28       | 82            | 24                   | Silo 3, Cold, Day 9, Rep 1  |
| S3CD9     | 28A      | 83            | 25                   | Silo 3, Cold, Day 9, Rep 2  |
| S9HD9     | 32       | 84            | 26                   | Silo 9, Hot , Day 9, Rep 1  |
| S9HD9     | 32A      | 85            | 27                   | Silo 9, Hot, Day 9, Rep 2   |
| S2CD11    | 35       | 86            | 28                   | Silo 2, Cold, Day 11, Rep 1 |
| S2CD11    | 35A      | 87            | 29                   | Silo 2, Cold, Day 11, Rep 2 |
| S3CD11    | 36       | 88            | 30                   | Silo 3, Cold, Day 11, Rep 1 |
| S3CD11    | 36A      | 89            | 31                   | Silo 3, Cold, Day 11, Rep 2 |
| S9HD11    | 40       | 90            | 32                   | Silo 9, Hot, Day 11, Rep 1  |
| S9HD11    | 40A      | 91            | 33                   | Silo 9, Hot, Day 11, Rep 2  |
| S2CD13    | 43       | 92            | 34                   | Silo 2, Cold, Day 13, Rep 1 |
| S2CD13    | 43A      | 93            | 35                   | Silo 2, Cold, Day 13, Rep 2 |
| S3CD13    | 44       | 94            | 36                   | Silo 3, Cold, Day 13, Rep 1 |
| S3CD13    | 44A      | 95            | 37                   | Silo 3, Cold, Day 13, Rep 2 |
| S9HD13    | 48       | 96            | 38                   | Silo 9, Hot, Day 13, Rep 1  |
| S9HD13    | 48A      | 97            | 39                   | Silo 9, Hot Day 13, Rep 2   |
| S2CD15    | 51       | 98            | 40                   | Silo 2, Cold, Day 15, Rep 1 |
| S2CD15    | 51A      | 99            | 41                   | Silo 2, Cold, Day 15, Rep 2 |
| S3CD15    | 52       | 100           | 42                   | Silo 3, Cold, Day 15, Rep 1 |
| S3CD15    | 52A      | 101           | 43                   | Silo 3, Cold, Day 15, Rep 2 |
| S9HD15    | 56       | 102           | 44                   | Silo 9, Hot, Day 15, Rep 1  |
| S9HD15    | 56A      | 103           | 45                   | Silo 9, Hot, Day 15, Rep 2  |

I then sorted the whole file from left to right (from lower to higher numerical values) using Row 1. This will put all my sample numbers in order.  

Here is my [file](https://github.com/Ellior2/Fish-546-Bioinformatics/blob/master/analyses/DDA_2016/Abacus_ADJNSAF.csv) 

__I ran the following code in R:__    

#to install packages   
install.packages("vegan")   
install.packages("raster")   
library(vegan)   
library(raster)   

#to input my data   
cg.reps<-read.csv('/Users/rhondae/Desktop/2016DDA/Abacus_3_5_17/ABACUS_ADJNSAF.csv',header=T,row.names=1)

#to calculate coefficient of variation across technical replicates for each biological replicate   
pool0<-cbind(cg.reps[2],cg.reps[3])   
S2CD3<-cbind(cg.reps[4],cg.reps[5])   
S3CD3<-cbind(cg.reps[6],cg.reps[7])   
S9HD3<-cbind(cg.reps[8],cg.reps[9])   
S2CD5<-cbind(cg.reps[10],cg.reps[11])   
S3CD5<-cbind(cg.reps[12],cg.reps[13])   
S9HD5<-cbind(cg.reps[14],cg.reps[15])   
S2CD7<-cbind(cg.reps[16],cg.reps[17])   
S3CD7<-cbind(cg.reps[18],cg.reps[19])   
S9HD7<-cbind(cg.reps[20],cg.reps[21])   
S2CD9<-cbind(cg.reps[22],cg.reps[23])   
S3CD9<-cbind(cg.reps[24],cg.reps[25])   
S9HD9<-cbind(cg.reps[26],cg.reps[27])   
S2CD11<-cbind(cg.reps[28],cg.reps[29])   
S3CD11<-cbind(cg.reps[30],cg.reps[31])   
S9HD11<-cbind(cg.reps[32],cg.reps[33])   
S2CD13<-cbind(cg.reps[34],cg.reps[35])   
S3CD13<-cbind(cg.reps[36],cg.reps[37])   
S9HD13<-cbind(cg.reps[38],cg.reps[39])   
S2CD15<-cbind(cg.reps[40],cg.reps[41])   
S3CD15<-cbind(cg.reps[42],cg.reps[43])   
S9HD15<-cbind(cg.reps[44],cg.reps[45])   

pool0.cv<-apply(pool0,1,cv)   
S2CD3.cv<-apply(S2CD3,1,cv)   
S3CD3.cv<-apply(S3CD3,1,cv)   
S9HD3.cv<-apply(S9HD3,1,cv)   
S2CD5.cv<-apply(S2CD5,1,cv)   
S3CD5.cv<-apply(S3CD5,1,cv)   
S9HD5.cv<-apply(S9HD5,1,cv)   
S2CD7.cv<-apply(S2CD7,1,cv)   
S3CD7.cv<-apply(S3CD7,1,cv)   
S9HD7.cv<-apply(S9HD7,1,cv)   
S2CD9.cv<-apply(S2CD9,1,cv)   
S3CD9.cv<-apply(S3CD9,1,cv)   
S9HD9.cv<-apply(S9HD9,1,cv)   
S2CD11.cv<-apply(S2CD11,1,cv)   
S3CD11.cv<-apply(S3CD11,1,cv)   
S9HD11.cv<-apply(S9HD11,1,cv)   
S2CD13.cv<-apply(S2CD13,1,cv)   
S3CD13.cv<-apply(S3CD13,1,cv)   
S9HD13.cv<-apply(S9HD13,1,cv)   
S2CD15.cv<-apply(S2CD15,1,cv)   
S3CD15.cv<-apply(S3CD15,1,cv)   
S9HD15.cv<-apply(S9HD15,1,cv)   

oyster.cv<-cbind(pool0.cv,S2CD3.cv,S3CD3.cv,S9HD3.cv,S2CD5.cv,S3CD5.cv,S9HD5.cv,S2CD7.cv,S3CD7.cv,S9HD7.cv,S2CD9.cv,S3CD9.cv,S9HD9.cv,S2CD11.cv,S3CD11.cv,S9HD11.cv,S2CD13.cv,S3CD13.cv,S9HD13.cv,S2CD15.cv,S3CD15.cv,S9HD15.cv)

boxplot(oyster.cv,outline=T,names=c('pool0','S2CD3','S3CD3','S9HD3','S2CD5','S3CD5','S9HD5','S2CD7','S3CD7','S9HD7','S2CD9','S3CD9','S9HD9','S2CD11','S3CD11','S9HD11','S2CD13','S3CD13','S9HD13','S2CD15','S3CD15','S9HD15'))

Here is the [boxplot](https://github.com/Ellior2/Fish-546-Bioinformatics/blob/master/analyses/DDA_2016/boxplot_reps.emf)



