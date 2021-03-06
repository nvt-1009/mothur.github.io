---
title: 'mothur v.1.7.0'
redirect_from: '/wiki/Mothur_v.1.7.0.html'
---
We hare happy to announce the release of [mothur
v.1.7.0](/wiki/mothur_v.1.7.0) in time for the US Thanksgiving
Holiday. So as you gather around the table and tell your family what you
are thankful for, be sure to thank your mothur. This has been a great
month for mothur. The manuscript describing mothur has been published in
[Applied & Environmental
Microbiology](https://aem.asm.org/cgi/content/abstract/75/23/7537). Also,
the manuscript describing the aligner that is used in mothur has been
accepted by PLoS ONE and will hopefully be posted soon. I give you full
permission to cite both liberally. Because of this we have had a fair
amount of traffic by people downloading mothur - so if this is your
first update, welcome. Many of you may remember that last month we
launched two new ventures a [facebook
page](https://www.facebook.com/pages/mothur/133966409231) and a [user
forum](https://forum.mothur.org). We are up to 53 "friends" and
have gotten a steady stream of forum users. Please feel free to use the
wiki, forum, and facebook as means of communicating with and helping
each other. December also promises to be a promising month as The
Mothur, is due to release dotur v.2.0 "Ruth" on December 6th.

This update has a number of features that people are sure to find
useful. First, we have added several commands for processing and
characterizing OTUs. Second, we have added an alternative algorithm for
clustering sequences using the furthest neighbor algorithm, which is
based on the algorithm described by [Sun and colleagues
(2009)](https://doi.org/10.1093/nar/gkp285). We
are unable to replicate the numbers they describe for mothur, so take
that part of their analysis with a grain of salt. What we have found is
that the memory requirements using the hcluster
command are minimal; however it tends to run a bit slower than the
cluster command. Finally and most significantly, we have added two
methods for classifying sequences - the k-Nearest Neighbor algorithm and
RDP's Bayesian Classifier. These data can then be used to assign
sequences to phylotypes. As with everything we do, our goal is to
provide the flexibility to use any classifier you want with any taxonomy
scheme you want. With these additions, we now have the ability to pursue
OTU, phylotype, and hypothesis testing-based approaches. We will
continue to add features, including those that you suggest, with the
goal of making mothur everything you need it to be.

## New commands

-   [get.otulist](/wiki/get.otulist) command - Outputs a .otu file
    for each distance specified containing the bin number and a list of
    the sequences in that bin.
-   hcluster command - clusters distance files of
    any size. It is slower than the [cluster](/wiki/cluster)
    command, which stores the distance in RAM to increase performance,
    so if you can fit your file in RAM use
    [cluster](/wiki/cluster).
-   [classify.seqs](/wiki/classify.seqs) command - classifies
    sequences using the knn or bayesian methods.
-   [phylotype](/wiki/phylotype) command - creates .list, .rabund
    and .sabund files from a taxonomy file.

## Updates

-   [read.otu](/wiki/read.otu) command - Added a groups parameter
    to specify which groups you would like to use.
-   [summary.shared](/wiki/summary.shared) and
    [collect.shared](/wiki/collect.shared) commands - added an all
    option, which estimates the combined richness of all your groups
    when using the [sharedchao](/wiki/sharedchao) and
    [sharedsobs](/wiki/sharedsobs) calculators.
-   [trim.seqs](/wiki/trim.seqs) command - Added a qtrim parameter,
    which gives an additional method of processing quality data.
-   [libshuff](/wiki/libshuff) command - Fixed a bug, which could
    affect P-values.
