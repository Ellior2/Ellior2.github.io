---

layout: post
title: What happens at Day 9? What are differences in protein expression between silos at Day 9?
---

04/30/2017

First I used Qspec to calculate statistics:

- First using [Qspec](http://www.nesvilab.org/qspec.php/) I calculated statistics associated with differential protein expression between Silo 2-23C and Silo 9-29C at Day 9. Here is the [file](https://github.com/RobertsLab/project-pacific.oyster-larvae/blob/master/DDA_2016/Qspec27.32.txt)

- [Here](https://github.com/RobertsLab/project-pacific.oyster-larvae/blob/master/DDA_2016/qspec.JPG) is what Qspec looks like.

- You will get an output with Z statistics and log fold change values. You want to consider all proteins with a Z-statistic with absolute value of at least 2 and a log fold change with an absolute value of at least 0.5.

- Next you will annotate this file by joining (I like to use [Galaxy](https://usegalaxy.org/). Here is the [file](https://github.com/RobertsLab/project-pacific.oyster-larvae/blob/master/DDA_2016/query_results.txt) I used to join with my [output file](https://github.com/RobertsLab/project-pacific.oyster-larvae/blob/master/DDA_2016/27.32results.txt) from Qspec. Here is a screenshot

- I first sorted the file using true values. The negative values represent highly expressed proteins in your "0" treatment- or your first column in the file you uploaded to Qspec. The positive values represent highly expressed proteins in your "1" treatment- or second column.

- The I seperated the file into two files- one with proteins highly expressed in my Silo 2-23C and one with proteins highly expressed in Silo 9-29C.

- Now for each file, I sorted to remove any proteins that did not fit the statistical criteria described above.

- I uploaded these two files in Galaxy and unfolded 