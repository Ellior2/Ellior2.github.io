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

I tried unfolding these GO terms in Galaxy but it appears their unfold function is not working. I posted an [issue #654](https://github.com/sr320/LabDocs/issues/654) on Github and Sam wrote up a bash script for me to use on this file. I followed the directions he wrote up. 

Here is my [unfold script](https://github.com/RobertsLab/project-pacific.oyster-larvae/blob/master/DIA_2015/unfold.sh).

This was my input file [AnnotatedproteinsGO.tabular](https://github.com/RobertsLab/project-pacific.oyster-larvae/blob/master/DIA_2015/AnnotatedproteinsGO.tabular) and here was my output file [unfolded.tab](https://github.com/RobertsLab/project-pacific.oyster-larvae/blob/master/DIA_2015/unfolded.tab)

Hooray!

In this step outlined above I had used a file where I had calculated the percent contribution of each sample to that protein. In these steps below, I repeat what I did above except I am using a file with the raw values for the "area" that I had gotten out of Skyline here:  https://github.com/RobertsLab/project-pacific.oyster-larvae/blob/master/DIA_2015/skylineoutput_wNA.xlsx

I followed the same steps above to unfold the GO column and then I merged with the [GOtoGOslim file](https://github.com/RobertsLab/project-pacific.oyster-larvae/blob/master/DDA_2016/GO_slim/Gotogoslim.txt) in Galaxy similar to what I did when analyzing the 2016 data found here: https://ellior2.github.io/GoSlimRedone/

Here is the file I am working with now: https://github.com/RobertsLab/project-pacific.oyster-larvae/blob/master/DIA_2015/AnnotatedproteinsGOarea.tabular.xlsx

Then I created a Pivot table to sum the areas:
![pivottable](https://raw.githubusercontent.com/Ellior2/Ellior2.github.io/master/images/screenshot2015goslim.JPG)


Here is a graph showing the GO slims for each of the four samples:
[Goslim 2015](https://raw.githubusercontent.com/Ellior2/Ellior2.github.io/master/images/2015GOslim.JPG)
![im](https://raw.githubusercontent.com/Ellior2/Ellior2.github.io/master/images/2015GOslim.JPG)

