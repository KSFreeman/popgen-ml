# popgen-ml

These scripts are used to implement [DiploSH/IC](http://www.g3journal.org/content/8/6/1959) on the [TTT_RecombinationGenomeScans data](https://github.com/TestTheTests/TTT_RecombinationGenomeScans/tree/master/results_final). The idea is to use the statistics calculated by various genome scans as features in a convolutional neural net (implemeneted in DiploSH/IC) in order to predict the genetic map. The current implementation classifies an entire chromosome as containing QTL sites, containing a selective sweep, under the effects of background selection, containing an inversion, containing an area of low recombination, or having a variable recombination rate.  A future version will classify each SNP in the set individaully as being in an inversion, being a QTL, etc.


## Overview of creating the feature vectors

1) Read the relevant genome scan statistics from each simulation

2) Split the statistics by chromosome

3) Split each chromosome into 11 windows (11 can be easily changed to a different number of windows)

4) For each window, calculate the mean value of each test statistic. If any mean is negative, add the smallest mean to every mean so that the smallest value is now 0. 

5) Divide each mean by the total of all the means. The statistics are now all between 0 and 1

6) Put these statistics into the appropriate feature vector file. There will be a file for neutral, low recombination, inversion etc.

## Genetic Map

![alt text](https://github.com/KSFreeman/popgen-ml/genetic_map.pdf)


## Format of feature vectors

The feature vectores have 99 columns and either 60 or 120 rows. Explanation:

`9 (number of stats) x 11 (number of windows) = 99 columns` 

`60 (number of sims) x 1 (number of chromosomes per sim that fall into each category) = 60 rows`
or 
`60 x 2 = 120 rows for neutral, QTL, background selection`


