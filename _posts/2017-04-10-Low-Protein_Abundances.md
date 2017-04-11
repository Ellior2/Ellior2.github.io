---

layout: post
title: 2016 Digging deeper into samples 35 and 43.
---

04/10/2017

## Samples 35 and 43- Low protein abundance

We noticed in the NMDS plot that samples 35 and 43 (which represent Silo 2- 23C at Day 11 and 13 when we were documenting high mortality) plotted farther away from the rest of the group. I looked further into the data for these samples and noticed two things:

- First, there were fewer overall proteins detected
- Second, for the proteins detected, there were fewer peptide matches for those proteins.

Emma reran some of the samples and did some of her own detection work:

From Emma:
This is what I have found on further analysis of your weird samples.

When I ran Rhonda's original data through the pipeline on our cluster, I got similar results: fewer proteins inferred in 35 and 43 than in 36 and 44.
35 & 35A: ~1900
36 & 36A: ~3400
43 & 43A: ~2500
44 & 44A: ~3200

I then ran a search that would allow for the identification of peptides with missed cleavages (possibly because of degradation). I did not see more missed cleavages/degradation in 35 & 43.  Here are the percentages of peptides with 1-9 missed cleavages:
35 & 35A: ~14%
36 & 36A: ~19%
43 & 43A: ~9%
44 & 44A: ~9%

These results are detailed in my evernote here.

We also re-ran samples 35 and 36 on the Q-Exactive to see if the same pattern was observed and if a greater injection volume would solve the issue. We injected both samples at 3 ul and then sample 35 at 9 ul.
We saw similar results to what we had seen on the Lumos.
TIC for 36 (3 ul): 1.25E10
TIC for 35 (3 ul): 8.11E9
TIC for 35 (9 ul): 9.63E9

A greater volume did not really increase the number of peptides or proteins identified. For sample 36, we found 7537 peptides and 1643 proteins. A higher volume injection of sample 35 raised the peptide count from 3420 to 3557 and the protein count from 1117 to 1202.

These results are detailed here.

At this point I do not think that sample degradation is the problem, although maybe there is a better way of detecting it than what I did. It is a little strange that a 3x volume didn't measurably increase our protein inferences, but that does suggest that there just aren't as many proteins in 35 and 43 (metabolic suppression may be a good hypothesis).


