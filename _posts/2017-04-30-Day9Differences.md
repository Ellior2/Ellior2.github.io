---

layout: post
title: What happened at Day 9?
---

04/30/2017

In the NMDS plot we noticed a divergence occuring at Day 9 between all of the silos. Here I compared Sample 27 (Silo 2-23C at Day 9) with 32 (Silo 9-29C at Day 9). See [table](https://github.com/RobertsLab/project-pacific.oyster-larvae/blob/master/DDA_2016/Qspec27.32DiffProteins_annotated.tabular)

I used Qspec to calculate statistics:

- First using [Qspec](http://www.nesvilab.org/qspec.php/) I calculated statistics associated with differential protein expression between Silo 2-23C and Silo 9-29C at Day 9. Here is the [file](https://github.com/RobertsLab/project-pacific.oyster-larvae/blob/master/DDA_2016/Qspec27.32.txt)

- [Here](https://github.com/RobertsLab/project-pacific.oyster-larvae/blob/master/DDA_2016/qspec.JPG) is what Qspec looks like.

- You will get an output with Z statistics and log fold change values. You want to consider all proteins with a Z-statistic with absolute value of at least 2 and a log fold change with an absolute value of at least 0.5.

- Next you will annotate this file by joining (I like to use [Galaxy](https://usegalaxy.org/)). Here is the [file](https://github.com/RobertsLab/project-pacific.oyster-larvae/blob/master/DDA_2016/query_results.txt) I used to join with my [output file](https://github.com/RobertsLab/project-pacific.oyster-larvae/blob/master/DDA_2016/27.32results.txt) from Qspec. 

![im](https://raw.githubusercontent.com/RobertsLab/project-pacific.oyster-larvae/master/DDA_2016/Galaxyjoin.JPG)

- After annotation I sorted the file using true values. The negative values represent highly expressed proteins in your "0" treatment- or your first column in the file you uploaded to Qspec. The positive values represent highly expressed proteins in your "1" treatment- or second column.

- The I seperated the file into two files- one with proteins highly expressed in my Silo 2-23C and one with proteins highly expressed in Silo 9-29C.

- Now for each file, I sorted to remove any proteins that did not fit the statistical criteria described above.

- I uploaded these two files in Galaxy and unfolded the GO column. 

![im](https://raw.githubusercontent.com/RobertsLab/project-pacific.oyster-larvae/master/DDA_2016/Galaxyunfold.JPG)

- Here are my two files:

[Silo 2-23C high expression](https://github.com/RobertsLab/project-pacific.oyster-larvae/blob/master/DDA_2016/Silo2-23Chighexp_unfold.tabular)

[Silo 9-29C high expression](https://github.com/RobertsLab/project-pacific.oyster-larvae/blob/master/DDA_2016/SIlo9-29Chighexp_unfold.tabular)

- Next I copied and pasted the GO terms and the associated Z-statistic to a new sheet. There were some proteins that were not annotated and so I deleted if there was no GO term associated with it for the [Revigo](http://revigo.irb.hr/revigo.jsp) analysis.

- Here are the Revigo visualizations

### Silo 2-23C Differentially expressed proteins

![im](https://raw.githubusercontent.com/RobertsLab/project-pacific.oyster-larvae/master/DDA_2016/Silo2-23CrevigoHighexp.JPG)


### Silo 9-29C Differentially expressed proteins

![im](https://raw.githubusercontent.com/RobertsLab/project-pacific.oyster-larvae/master/DDA_2016/Silo9-29CrevigoHighexp.JPG)
