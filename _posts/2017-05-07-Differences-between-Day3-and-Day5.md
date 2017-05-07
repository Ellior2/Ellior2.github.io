---

layout: post
title: Differences in protein expression between Day 3 and Day 5
---

05/07/17

In this post I am seeking to understand the differences in protein expression exhibited by all silos between Day 3 and Day 5. In these earlier development stages all silos seem to cluster closely together on each day so I decided to treat all silos as "biological replicates" for Day 3 and compare to the same replicates at Day 5. By asking these questions we should be able to uncover important proteins that oysters are expressing during the settlement phase.


I followed a similar protocol as discussed [here](https://ellior2.github.io/Day9Differences/).

The [file](https://github.com/RobertsLab/project-pacific.oyster-larvae/blob/master/DDA_2016/Abacus/ABACUS_NUMSPECSTOT_3%2C4%2C8vs11%2C12%2C16.txt) I submitted to Qspec:

The [output file](https://github.com/RobertsLab/project-pacific.oyster-larvae/blob/master/DDA_2016/Qspec3%2C4%2C8vs11%2C12%2C16/qspec3%2C4%2C8vs11%2C12%2C16.xlsx)

Then I kept all proteins detected with a Z-statistic with absolute value above 2 and a log fold change with absolute value above 0.5.

I split the file and seperated the proteins highly expressed at Day 3 from the proteins highly expressed at Day 5.

[Day 3 Highly expressed proteins](https://github.com/RobertsLab/project-pacific.oyster-larvae/blob/master/DDA_2016/Qspec3%2C4%2C8vs11%2C12%2C16/HighexpatDay3_annotated.tabular.txt)

[Day 5 Highly expressed proteins](https://github.com/RobertsLab/project-pacific.oyster-larvae/blob/master/DDA_2016/Qspec3%2C4%2C8vs11%2C12%2C16/HighexpatDay5_annotated.tabular.txt)


I uploaded the annotated files to Galaxy and unfolded the GO column.

[Day 3 unfolded GO terms](https://github.com/RobertsLab/project-pacific.oyster-larvae/blob/master/DDA_2016/Qspec3%2C4%2C8vs11%2C12%2C16/HighexpatDay3_annotated_unfolded.tabular)

[Day 5 unfolded GO terms](https://github.com/RobertsLab/project-pacific.oyster-larvae/blob/master/DDA_2016/Qspec3%2C4%2C8vs11%2C12%2C16/HighexpatDay5_annotated_unfolded.tabular)

Here are Revigo visualizations

High protein expression at Day 3 for all silos
![im](https://raw.githubusercontent.com/RobertsLab/project-pacific.oyster-larvae/master/DDA_2016/Qspec3%2C4%2C8vs11%2C12%2C16/HighexpatDay3Revigo.JPG)


High protein expression at Day 5 for all silos
![im](https://raw.githubusercontent.com/RobertsLab/project-pacific.oyster-larvae/master/DDA_2016/Qspec3%2C4%2C8vs11%2C12%2C16/HighexpatDay5Revigo.JPG)