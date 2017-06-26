---

layout: post
title: GOSlim redone
---

06/25/17

I am going to manually join my result tables with the GOtoGOslim table.

First I took the full list of all proteins detected in my samples found [here](https://github.com/RobertsLab/project-pacific.oyster-larvae/blob/master/DDA_2016/completeCHOYPproteins.txt) and uploaded it into [Galaxy](usegalaxy.org).

Then I joined this file with the [Gigaton-BlastUniprot](https://github.com/RobertsLab/project-pacific.oyster-larvae/blob/master/DDA_2016/GO_slim/blastoutputgigaton.txt) file found on SQL share. This is getting me from the CHOYP.... protein labels to the 6 character code that identifies the protein. 

From this file I joined it to a table with GO terms- uniprot-all.tab downloaded from http://www.uniprot.org/

Because each protein corresponds with multiple GO terms I had to unfold the GO term column to put each GO term on a seperate line using Galaxy.

I had to remove leading white spaces from these unfolded terms and did so in excel using the TRIM function. See [here](https://github.com/RobertsLab/project-pacific.oyster-larvae/blob/master/DDA_2016/GO_slim/unfoldedcompletegoterms.tabular)

Then I joined this table with the [GOtoGOslim](https://github.com/RobertsLab/project-pacific.oyster-larvae/blob/master/DDA_2016/GO_slim/Gotogoslim.txt) table and ended up with this [file](https://github.com/RobertsLab/project-pacific.oyster-larvae/blob/master/DDA_2016/GO_slim/Allsamples_Goslimjoin.interval) where I have the CHOYP proteins, NSAF values for all samples, all GO terms, and all GO slim terms.

Yay! Now it's just a matter of making some visualizations.