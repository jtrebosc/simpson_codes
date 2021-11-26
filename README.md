# Simpson codes
[simpson](https://inano.au.dk/about/research-centers-and-projects/nmr/software/simpson/) is an NMR simulation program taking specific tcl scripts as input files.
This repository contains simpson input codes doing various nmr simulations.

A few codes may require specific version of simpson program (such as [simpsonJT](https://github.com/jtrebosc/simpson/tree/MasterJT))
or additionnal library ([opt](https://inano.au.dk/fileadmin/_migrated/content_uploads/opt-1.0.zip)).

## FAMN\_opt
FAM-N is a method to enhance magnetization transfer between 3Q and 1Q coherence levels, used for reconversion in an MQMAS experiment. 
It was designed by [Henri Colaux et al. in 2014](https://doi.org/10.1021/jp505752c) and [further studied in 2017](https://doi.org/10.1016/j.ssnmr.2017.01.001). 
Optimization was done using matlab code calling externaly simpson.

This code performs FAM-N optimization from a single simpson input file. The result of optimization is printed on screen. It can use all simpson features 
in terms of averaging over different parameters like quadrupolar parameters or RF field profiles.

This code requires [simpsonJT](https://github.com/jtrebosc/simpson/tree/MasterJT) version and the [opt](https://inano.au.dk/fileadmin/_migrated/content_uploads/opt-1.0.zip) 
library located in the same directory as the simpson input file.

### Usage:
Input parameters are all located at start of input file in spinsys and par section like nucleus of interest, quadrupolar interaction characteristics, 
spinning speed, RF field, 1H larmor frequency for the most important ones.
One new feature is that optimization can give some weight to the final pulse length. This can be of interest to limit spectral distorsions
induced by long pulses when the gain of extra pulses makes the train much longer.

Specific FAM-N parameters are :
* nQ: the nQMAS level : 3, 5, 7, 9 for 3QMAS, 5QMAS...
* n\_of\_pulses\_max: limit the maximum of number pulses
* PLweight: pulse length weighting parameter. If 0, pulse length does not affect the optimum, increasing values will try to minimize the pulse length
trading off transfer efficiency.
* min\_pulse\_length: pulse length cannot be smaller than that parameter 
* max\_pulse\_length: pulse length cannot be larger than that parameter 
* pulse\_step: parameter used by minimizing library

