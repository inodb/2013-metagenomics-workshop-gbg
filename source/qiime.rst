==============================================================
Quantitative Insights Into Microbial Ecology (QIIME) Practical
==============================================================

The Data
========
A research group has performed a 16S rRNA amplification protocol to some
sediment samples, which were sequenced on an Illumina machine. Here we will see
which species of bacteria are present in the sediments by using some steps of
the Qiime pipeline. 

During the exercise we will refer to this tutorial
http://qiime.org/tutorials/tutorial.html, so you can read in more detail the
steps and parameters followed here.

Unfortunately you will not be running the different steps, however we provide you with all the command lines used in this pracical (qiime.sh)

You will find the data at ``rudy``. The raw data:

``seqs.fa``
    sequencing reads, already demultiplexed and formatted for processing
    http://qiime.org/tutorials/tutorial.html#assign-samples-to-multiplex-reads

``Map.txt``
    sample description 
    http://qiime.org/tutorials/tutorial.html#mapping-file-tab-delimited-txt

``qiime.sh``
    batch script that runs some steps for de novo OUT picking and diversity
    analyses

Under the Files folder you will find reference files used by Qiime for the
analysis of your reads. As you progress in the exercise, remember to check what
are these files used for::

    97_otus.fasta  
    97_otu_taxonomy.txt  
    core_set_aligned.fasta.imputed  
    gg_97_otus_4feb2011_aligned.fasta 
    greengenes_tax_rdp_train.txt  
    lanemask_in_1s_and_0s

Installing required software
============================

To inspect the different results, you need to install the following software in
your computer, not in the server!:

KiNG
    an interactive system for three-dimensional vector graphics) 
    http://kinemage.biochem.duke.edu/software/king.php

FigTree
    a graphical viewer of phylogenetic trees
    http://tree.bio.ed.ac.uk/software/figtree/

Picking operational taxonomic units
===================================

Go to
http://qiime.org/tutorials/tutorial.html#picking-operational-taxonomic-units-otus-through-making-otu-table.
Read through and inspect the files created in this section under ``OTUS/``. To look at the
phylogenetic tree, use FigTree
to open ``rep_set.tree``

Viewing statistics
==================

Go to http://qiime.org/tutorials/tutorial.html#view-statistics-of-the-otu-table

Are the reads from all the samples evenly distributed? Should they be?

Out heatmap
===========

Go to http://qiime.org/tutorials/tutorial.html#make-otu-heatmap. Open ``otu_table.html`` from 
``OTUS/OTU_heatmap/`` in a web
browser.

What can you conclude from these results?

Taxonomic composition
=====================

Go to
http://qiime.org/tutorials/tutorial.html#summarize-communities-by-taxonomic-composition.
Compare ``area_charts.html`` and
``bars_charts.html`` from ``wf_taxa_summary/``  

Is the distribution of organisms similar/different among samples?

Alpha diversity and rarefaction curves
======================================

Go to
http://qiime.org/tutorials/tutorial.html#compute-alpha-diversity-within-the-samples-and-generate-rarefaction-curves
. Open ``rarefaction_plots.html`` from ``wf_arare/`` and inspect the observed_species
metric vs depth, dissolved_oxigen and temperature. 

What are your conclusions? 

Beta diversity
==============

Go to
http://qiime.org/tutorials/tutorial.html#compute-beta-diversity-and-generate-beta-diversity-plots.
Inspect the PCoA plots from the weighted and unweighted
comparisons from ``wf_bdiv/``. You can either look at the 2D (web browser) or 3D PCoA plots
(using KiNG). 

Are there any differences between the clustering of weighted and unweighted versions?

Estimating the precision of sample statistics and hierarchical clustering
==========================================================================

Go to http://qiime.org/tutorials/tutorial.html#jackknifed-beta-diversity-and-hierarchical-clustering. Look under ``wf_jack/``. 

Which version, weighted or unweighted, shows more support in their internal
nodes?  Which is the more reliable clustering? Look at the pdf files
(``jackknife_named_nodes.pdf``)
