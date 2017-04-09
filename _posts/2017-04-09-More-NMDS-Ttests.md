---

layout: post
title: 2016 Data Processing-More NMDS
---

04/09/2017

### More NMDS and Paired T-tests to compare technical reps

I made a nicer NMDS in R using some fun shapes and colors of the rainbow.

install.packages("vegan")   
library(vegan)   
install.packages("raster")  
library(raster)  


#I used the GUI interface, looked on Packages Tab to find Install Packages. Then I selected BioStatR.
#Then I loaded the biostats package.

source('~/GitHub/Fish-546-Bioinformatics/analyses/DDA_2016/biostats.R', encoding = 'UTF-8')

cg.reps<-read.csv('/Users/rhondae/Documents/Github/Fish-546-Bioinformatics/analyses/DDA_2016/ABACUS_ADJNSAF_NMDS.csv',header=T,row.names=1)

pool0<-cbind(cg.reps[1],cg.reps[2])
S2CD3<-cbind(cg.reps[3],cg.reps[4])
S3CD3<-cbind(cg.reps[5],cg.reps[6])
S9HD3<-cbind(cg.reps[7],cg.reps[8])
S2CD5<-cbind(cg.reps[9],cg.reps[10])
S3CD5<-cbind(cg.reps[11],cg.reps[12])
S9HD5<-cbind(cg.reps[13],cg.reps[14])
S2CD7<-cbind(cg.reps[15],cg.reps[16])
S3CD7<-cbind(cg.reps[17],cg.reps[18])
S9HD7<-cbind(cg.reps[19],cg.reps[20])
S2CD9<-cbind(cg.reps[21],cg.reps[22])
S3CD9<-cbind(cg.reps[23],cg.reps[24])
S9HD9<-cbind(cg.reps[25],cg.reps[26])
S2CD11<-cbind(cg.reps[27],cg.reps[28])
S3CD11<-cbind(cg.reps[29],cg.reps[30])
S9HD11<-cbind(cg.reps[31],cg.reps[32])
S2CD13<-cbind(cg.reps[33],cg.reps[34])
S3CD13<-cbind(cg.reps[35],cg.reps[36])
S9HD13<-cbind(cg.reps[37],cg.reps[38])
S2CD15<-cbind(cg.reps[39],cg.reps[40])
S3CD15<-cbind(cg.reps[41],cg.reps[42])
S9HD15<-cbind(cg.reps[43],cg.reps[44])

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



#NMDS
reps.t<-t(cg.reps)
reps.tra<-(reps.t+1)
reps.tra<-data.trans(reps.tra, method='log', plot=F)

#assign colors to reps
reps.nmds<-metaMDS(reps.tra, distance='bray', k=2, trymax=100, autotransform=F)
fig.reps<-ordiplot(reps.nmds, choices=c(1,2), type='none', display='sites', xlab='Axis 1', ylab='Axis 2', cex=0.5)
points(fig.reps, 'sites', col=c(rep('black',2), rep('red',2), rep('red',2), rep('red',2), rep('orange',2), rep('orange',2), rep('orange',2),rep('yellow',2), rep('yellow',2), rep('yellow',2), rep('green',2),rep('green',2),rep('green',2), rep('blue',2),rep('blue',2),rep('blue',2),rep('darkslateblue',2),rep('darkslateblue',2),rep('darkslateblue',2),rep('purple',2),rep('purple',2),rep('purple',2)), pch=c(rep(18,2), rep(19,2), rep(15,2), rep(17,2), rep(19,2), rep(15,2),rep(17,2), rep(19,2), rep(15,2), rep(17,2), rep(19,2), rep(15,2), rep(17,2), rep(19,2), rep(15,2), rep(17,2),rep(19,2), rep(15,2), rep(17,2), rep(19,2), rep(15,2), rep(17,2)))
legend("topright", legend=c("pool0","23C-Silo2", "23C-Silo3", "29C-Silo9"), pch=c(18,19,15,17))
#Day 0=black, Day 3=red, Day 5=orange, Day 7=yellow, Day 9=green, Day 11=blue, Day 13=indigo, Day 15=purple
#pool0= diamonds, 23C-Silo 2 = circles, 23C-Silo 3= square, 29-Silo 9 = triangles


![NMDS](https://raw.githubusercontent.com/Ellior2/Fish-546-Bioinformatics/master/analyses/DDA_2016/NMDSplot.JPG)


#paired t-test to compare my technical replicates. If not statistically different, I will combine.
> t.test(cg.reps[,1],cg.reps[,2],paired=T)

	Paired t-test

data:  cg.reps[, 1] and cg.reps[, 2]
t = 2.1387e-06, df = 8442, p-value = 1
alternative hypothesis: true difference in means is not equal to 0
95 percent confidence interval:
 -0.3473807  0.3473815
sample estimates:
mean of the differences 
           3.790122e-07 

> t.test(cg.reps[,1],cg.reps[,2],paired=T)

	Paired t-test

data:  cg.reps[, 1] and cg.reps[, 2]
t = 2.1387e-06, df = 8442, p-value = 1
alternative hypothesis: true difference in means is not equal to 0
95 percent confidence interval:
 -0.3473807  0.3473815
sample estimates:
mean of the differences 
           3.790122e-07 

> t.test(cg.reps[,3],cg.reps[,4],paired=T)

	Paired t-test

data:  cg.reps[, 3] and cg.reps[, 4]
t = 4.5054e-06, df = 8442, p-value = 1
alternative hypothesis: true difference in means is not equal to 0
95 percent confidence interval:
 -0.2370504  0.2370515
sample estimates:
mean of the differences 
             5.4483e-07 

> t.test(cg.reps[,5],cg.reps[,6],paired=T)

	Paired t-test

data:  cg.reps[, 5] and cg.reps[, 6]
t = -7.4438e-07, df = 8442, p-value = 1
alternative hypothesis: true difference in means is not equal to 0
95 percent confidence interval:
 -0.4366628  0.4366625
sample estimates:
mean of the differences 
          -1.658178e-07 

> t.test(cg.reps[,7],cg.reps[,8],paired=T)

	Paired t-test

data:  cg.reps[, 7] and cg.reps[, 8]
t = -3.4871e-06, df = 8442, p-value = 1
alternative hypothesis: true difference in means is not equal to 0
95 percent confidence interval:
 -0.2729844  0.2729834
sample estimates:
mean of the differences 
          -4.856094e-07 

> t.test(cg.reps[,9],cg.reps[,10],paired=T)

	Paired t-test

data:  cg.reps[, 9] and cg.reps[, 10]
t = 3.7229e-06, df = 8442, p-value = 1
alternative hypothesis: true difference in means is not equal to 0
95 percent confidence interval:
 -0.2993422  0.2993434
sample estimates:
mean of the differences 
           5.685183e-07 

> t.test(cg.reps[,11],cg.reps[,12],paired=T)

	Paired t-test

data:  cg.reps[, 11] and cg.reps[, 12]
t = -7.6365e-06, df = 8442, p-value = 1
alternative hypothesis: true difference in means is not equal to 0
95 percent confidence interval:
 -0.2189037  0.2189020
sample estimates:
mean of the differences 
          -8.527774e-07 

> t.test(cg.reps[,13],cg.reps[,14],paired=T)

	Paired t-test

data:  cg.reps[, 13] and cg.reps[, 14]
t = 2.8733e-06, df = 8442, p-value = 1
alternative hypothesis: true difference in means is not equal to 0
95 percent confidence interval:
 -0.3636197  0.3636207
sample estimates:
mean of the differences 
           5.329859e-07 

> t.test(cg.reps[,15],cg.reps[,16],paired=T)

	Paired t-test

data:  cg.reps[, 15] and cg.reps[, 16]
t = -4.4421e-06, df = 8442, p-value = 1
alternative hypothesis: true difference in means is not equal to 0
95 percent confidence interval:
 -0.1881590  0.1881581
sample estimates:
mean of the differences 
          -4.263887e-07 

> t.test(cg.reps[,17],cg.reps[,18],paired=T)

	Paired t-test

data:  cg.reps[, 17] and cg.reps[, 18]
t = -1.0711e-06, df = 8442, p-value = 1
alternative hypothesis: true difference in means is not equal to 0
95 percent confidence interval:
 -0.3468358  0.3468354
sample estimates:
mean of the differences 
          -1.895061e-07 

> t.test(cg.reps[,19],cg.reps[,20],paired=T)

	Paired t-test

data:  cg.reps[, 19] and cg.reps[, 20]
t = -1.2193e-06, df = 8442, p-value = 1
alternative hypothesis: true difference in means is not equal to 0
95 percent confidence interval:
 -0.2285081  0.2285078
sample estimates:
mean of the differences 
          -1.421296e-07 

> t.test(cg.reps[,21],cg.reps[,22],paired=T)

	Paired t-test

data:  cg.reps[, 21] and cg.reps[, 22]
t = -9.1564e-07, df = 8442, p-value = 1
alternative hypothesis: true difference in means is not equal to 0
95 percent confidence interval:
 -0.3042784  0.3042781
sample estimates:
mean of the differences 
          -1.421296e-07 

> t.test(cg.reps[,23],cg.reps[,24],paired=T)

	Paired t-test

data:  cg.reps[, 23] and cg.reps[, 24]
t = 1.8056e-06, df = 8442, p-value = 1
alternative hypothesis: true difference in means is not equal to 0
95 percent confidence interval:
 -0.3471845  0.3471851
sample estimates:
mean of the differences 
           3.197915e-07 

> t.test(cg.reps[,25],cg.reps[,26],paired=T)

	Paired t-test

data:  cg.reps[, 25] and cg.reps[, 26]
t = -3.3189e-06, df = 8442, p-value = 1
alternative hypothesis: true difference in means is not equal to 0
95 percent confidence interval:
 -0.3497770  0.3497758
sample estimates:
mean of the differences 
          -5.922066e-07 

> t.test(cg.reps[,27],cg.reps[,28],paired=T)

	Paired t-test

data:  cg.reps[, 27] and cg.reps[, 28]
t = -4.3921e-07, df = 8442, p-value = 1
alternative hypothesis: true difference in means is not equal to 0
95 percent confidence interval:
 -0.2643070  0.2643069
sample estimates:
mean of the differences 
          -5.922066e-08 

> t.test(cg.reps[,29],cg.reps[,30],paired=T)

	Paired t-test

data:  cg.reps[, 29] and cg.reps[, 30]
t = -1.9551e-06, df = 8442, p-value = 1
alternative hypothesis: true difference in means is not equal to 0
95 percent confidence interval:
 -0.3325056  0.3325050
sample estimates:
mean of the differences 
          -3.316357e-07 

> t.test(cg.reps[,31],cg.reps[,32],paired=T)

	Paired t-test

data:  cg.reps[, 31] and cg.reps[, 32]
t = 3.3094e-06, df = 8442, p-value = 1
alternative hypothesis: true difference in means is not equal to 0
95 percent confidence interval:
 -0.3928771  0.3928784
sample estimates:
mean of the differences 
           6.632713e-07 

> t.test(cg.reps[,33],cg.reps[,34],paired=T)

	Paired t-test

data:  cg.reps[, 33] and cg.reps[, 34]
t = -2.2423e-06, df = 8442, p-value = 1
alternative hypothesis: true difference in means is not equal to 0
95 percent confidence interval:
 -0.3727543  0.3727535
sample estimates:
mean of the differences 
          -4.263887e-07 

> t.test(cg.reps[,35],cg.reps[,36],paired=T)

	Paired t-test

data:  cg.reps[, 35] and cg.reps[, 36]
t = 4.0053e-07, df = 8442, p-value = 1
alternative hypothesis: true difference in means is not equal to 0
95 percent confidence interval:
 -0.2898311  0.2898312
sample estimates:
mean of the differences 
           5.922066e-08 

> t.test(cg.reps[,37],cg.reps[,38],paired=T)

	Paired t-test

data:  cg.reps[, 37] and cg.reps[, 38]
t = -3.6668e-06, df = 8442, p-value = 1
alternative hypothesis: true difference in means is not equal to 0
95 percent confidence interval:
 -0.4052324  0.4052309
sample estimates:
mean of the differences 
          -7.580244e-07 

> t.test(cg.reps[,39],cg.reps[,40],paired=T)

	Paired t-test

data:  cg.reps[, 39] and cg.reps[, 40]
t = -1.0939e-06, df = 8442, p-value = 1
alternative hypothesis: true difference in means is not equal to 0
95 percent confidence interval:
 -0.2334634  0.2334631
sample estimates:
mean of the differences 
          -1.302854e-07 

> t.test(cg.reps[,41],cg.reps[,42],paired=T)

	Paired t-test

data:  cg.reps[, 41] and cg.reps[, 42]
t = 3.4987e-06, df = 8442, p-value = 1
alternative hypothesis: true difference in means is not equal to 0
95 percent confidence interval:
 -0.3384338  0.3384350
sample estimates:
mean of the differences 
           6.040507e-07 

> t.test(cg.reps[,43],cg.reps[,44],paired=T)

	Paired t-test

data:  cg.reps[, 43] and cg.reps[, 44]
t = 9.471e-07, df = 8442, p-value = 1
alternative hypothesis: true difference in means is not equal to 0
95 percent confidence interval:
 -0.4167427  0.4167431
sample estimates:
mean of the differences 
           2.013502e-07 


There is no statistical difference between any of my technical replicates so I can combine!