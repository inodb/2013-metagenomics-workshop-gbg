==========================================
Assembling reads with Velvet
==========================================
In this exercise we will learn how to perform an assembly with Velvet. Velvet
takes your reads as input and turns them into contigs. It consists of two
steps. In the first step, ``velveth``, the de Bruijn graph is created.
Afterwards the graph is traversed and contigs are created with ``velvetg``.
When constructing the de Bruijn graph, a *kmer* has to be specified. Reads are
cut up into pieces of length *k*, each representing a node in the graph, edges
represent an overlap (some de Bruijn graph assemblers do this differently, but
the idea is the same). The advantage of using kmer overlap instead of read
overlap is that the computational requirements grow with the number of unique
kmers instead of unique reads. A more detailled explanation can be found at
http://www.nature.com/nbt/journal/v29/n11/full/nbt.2023.html.


Pick a kmer
===========
Please work in pairs for this assignment. Every group can select a kmer of
their likings - pick a random one if you haven't developed a preference yet.
Write you and your partner's name down at a kmer on
https://docs.google.com/spreadsheet/ccc?key=0AvduvUOYAB-_dDJwcG1jbk1kTTY3eGZNazJGMUhfM3c#gid=3.

velveth
=======
Create the graph data structure with ``velveth``. Again like we did with
``sickle``, first create a directory with symbolic links to the pairs that you
want to use::

    mkdir -p ~/metagenomics-workshop-gbg/velvet
    cd ~/metagenomics-workshop-gbg/velvet
    ln -s ../sickle/qtrim1.fastq pair1.fastq
    ln -s ../sickle/qtrim2.fastq pair2.fastq

The reads need to be interleaved for ``velveth``::

    shuffleSequences_fastq.pl pair1.fastq pair2.fastq pair.fastq

Run velveth over the kmer you picked (21 in the example)::

    velveth out_21 21 -fastq -shortPaired pair.fastq

Check what directories have been created::

    ls

velvetg
=======
To get the actual contigs you will have to run ``velvetg`` on the created
graph. You can vary options such expected coverage and the coverage cut-off if
you want, but we do not do that in this tutorial. We only choose not to do
scaffolding::

    velvetg out_21 -scaffolding no


assemstats
==========
After the assembly one wants to look at the length distributions of the
resulting assemblies. You can use the ``assemstats`` script for that::

    assemstats 100 out_*/contigs.fa

This part is optional. I usually look at the distributions setting the cut-off
at 100 and 1000 and put the results in google docs. A useful program for
copying the results from assemstats is ``xclip``. This can copy the results to
your clipboard so you can directly past the results into google docs::

    assemstats 100 out_*/contigs.fa | xclip -selection clipboard


Note that ``xclip`` requires you to log in with X-forwarding enabled, i.e.
``ssh -X inod@kalkyl1.uppmax.uu.se``.
