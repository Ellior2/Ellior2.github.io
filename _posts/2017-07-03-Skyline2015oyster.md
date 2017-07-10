---

layout: post
title: Skyline 2015 oyster seed experiment
---

07/03/17

I will be getting back into Skyline to analyze 2015 oyster seed experiment results.

I had to redownload the program and did so here: https://skyline.ms/project/home/software/Skyline/begin.view

I downloaded the version 3.7- 64bit

Since I had already done some work on this project back in October I am picking up where I left off.

Here is my [skyline output file](https://github.com/Ellior2/Fish-546-Bioinformatics/blob/master/analyses/taylor/proteomeoutput.csv) from before. It contains CGI_... codes.

Here is what the file looks before modification:

![step1](https://raw.githubusercontent.com/Ellior2/Ellior2.github.io/master/images/7_9_17post/step1.JPG)


First I removed all of the #N/A and replaced with blanks.

![step2](https://raw.githubusercontent.com/Ellior2/Ellior2.github.io/master/images/7_9_17post/step2.JPG)

Then I created a Pivot table to sum the peak areas for each protein across all samples

![step3](https://raw.githubusercontent.com/Ellior2/Ellior2.github.io/master/images/7_9_17post/step3.JPG)

Then I copied and pasted the results from the Pivot table to a new sheet to make it easier to work with.

![step4](https://raw.githubusercontent.com/Ellior2/Ellior2.github.io/master/images/7_9_17post/step4.JPG)

I summed up all the areas for each protein across all samples. To look at the relative abundance of proteins between samples, I created 4 extra columns that calculate the percent contribution each sample has to that protein. For example, for Oyster sample 1, I took the Oyster 1 summed area and divided it by the total summed area across all samples and muliplied by 100. I also relabeled the oyster sample #'s with their identification from the experiment.

Finally I sorted the file by summed area column for all samples largest to smallest to orient the most abundant proteins towards the top of the file.


![step5](https://raw.githubusercontent.com/Ellior2/Ellior2.github.io/master/images/7_9_17post/step5.JPG)

I copied and pasted these calculated percentages for each protein into a new file located [here](https://github.com/RobertsLab/project-pacific.oyster-larvae/blob/master/DIA_2015/RelativeabundanceCGI.txt).

I joined it with [Uniprot database with CGI codes and GO terms](https://github.com/Ellior2/Fish-546-Bioinformatics/blob/master/analyses/taylor/uniprot-cgi_GO.tab) in Galaxy.

![step6](https://raw.githubusercontent.com/Ellior2/Ellior2.github.io/master/images/7_9_17post/step6.JPG)


Here is the annotated [Excel file](https://github.com/RobertsLab/project-pacific.oyster-larvae/blob/master/DIA_2015/AnnotatedproteinsGO.tabular.xlsx) with all of the proteins detected among the four samples with corresponding GO terms.

