---
layout: post
title: Intro to Skyline
---

10/7/2016

## Skyline tutorial with Emma

Downloaded Skyline (version 3.5.0.9319) 9/27/16 

Downloaded WinSCP (version 5.9.2) on 10/7/16 to get raw files from Emma including 1 FASTA File (background proteome), and all 16 RAW files (4 per oyster sample). See Jupyter notebook for layout: Rawoysterfiles
1 PROTB File which we acquired through Skyline from the FASTA file

Now, with your BLIB library file (oysterseed2.blib) you should have everything you need to follow the slideshow tutorial for Skyline steps 2-6.

After you finish with Step 6 you will have imported the raw DIA data into skyline. There will be two windows open, go ahead and exit out of the one that is not your MS1 and MS2 scans for each oyster sample(Probably will show up on the right side). Instead you will want to add two more windows: Retention Times and Peak Area. Go to View>Retention times>Replicate Comparison and then View>Peak Areas>Replicate Comparison.

Arrange graphs- tiled if you want to see each sample separately although this may clutter up your screen.

To see both MS1 (precursor ions) and MS2 (transition) scans:
View>Transitions>All
View>Transitions>Split graphs

To export file as a CSV
File>Export>Reports

Then select Edit list, then ADD, then select the following:
1)	Proteins>Protein name
2)	Proteins>Peptides>Peptide sequence
3)	Proteins>Peptides>Average retention time 
4)	Proteins>Peptides>Precursors>Transitions>Transition Results> Area
5)	Proteins>Peptides>Precursors>Transitions>Fragment Ion Type
6)	Replicates>Replicate Name

Name your file and choose the location where you want it saved. Select preview and then you can export directly the preview page.

Then you will also want to Export Peptide RT results as a CSV file.

File>Export>Reports 	Then select Peptide RT results

Next steps:

Determine the coefficient of variation for the retention times for each peptide across oyster replicates.

Determine your error by choosing 100 random peptides and counting how many times Skyline incorrectly matched peaks or did not get entire peak area in the peak picking borders.

Learn MS stats (R-based package). This will help you figure out differentially abundant peptides and proteins and make some nice plots. Skyline daily has a pre-made export format for MSStats, but you will just need to look up the MSstats manual and figure it out if you don’t want to use daily  I also just learned that “group comparison” in Skyline will do a MSstats analysis, but without the nice graphs you get in the R package. Your call. 

Read Skyline tutorial (just the DIA one I sent)
