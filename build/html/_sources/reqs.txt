==========================================
Checking required software
==========================================
An often occuring theme in bioinformatics is installing software. Here we wil
go over some steps to help you check whether you actually have the right
software installed. There's an optional excerise on how to install ``sickle``.

Programs used in this workshop
==============================
The following programs are used in this workshop:

    - Bowtie2_
    - Velvet_
    - xclip_
    - parallel_
    - samtools_
    - CD-HIT_
    - AMOS_
    - sickle_
    - Picard_
    
.. _Bowtie2: http://bowtie-bio.sourceforge.net/bowtie2/index.shtml
.. _Velvet: http://www.ebi.ac.uk/~zerbino/velvet/
.. _xclip: http://sourceforge.net/projects/xclip/
.. _parallel: https://www.gnu.org/software/parallel/
.. _samtools: http://samtools.sourceforge.net/
.. _CD-HIT: https://code.google.com/p/cdhit/
.. _AMOS: http://sourceforge.net/apps/mediawiki/amos/index.php?title=AMOS
.. _sickle: https://github.com/najoshi/sickle
.. _Picard: http://picard.sourceforge.net/index.shtml

All programs are already installed, all you have to do is load the virtual
environment for this workshop. Once you are logged in to the server run::

    source /home/teacher8/virt_env/mg-workshop/bin/activate

You deactivate the virtual environment with::
    
    deactivate

NOTE: This is a python virtual environment. The binary folder of the virtual
environment has symbolic links to all programs used in this workshop so you
should be able to run those without problems.


Using which to locate a program
===============================
An easy way to determine whether you have have a certain program installed is
by typing::

    which programname
    
where ``programname`` is the name of the program you want to use. The program
``which`` searches all directories in ``$PATH`` for the executable file
``programname`` and returns the path of the first found hit. This is exactly
what happens when you would just type ``programname`` on the command line, but
then ``programname`` is also executed. To see what your ``$PATH`` looks like,
simply ``echo`` it::
    
    echo $PATH

Now check if you have xclip installed::

    $ which xclip
    /usr/bin/xclip

It doesn't matter if the path outputted by ``which`` is different for you as
long as you see a location of the program. No output means you don't have it in
your ``$PATH`` variable.

Check all programs in one go using xclip and which
==================================================
To check whether you have all programs installed in one go, you can use
``xclip`` and ``which``. Make sure you have xclip installed. Then copy this list
of programs and scripts that we will be using::

    xclip
    bowtie2
    bowtie2-build
    velveth
    velvetg
    shuffleSequences_fastq.pl
    parallel
    samtools
    toAmos
    minimus2

The command::
    
    xclip -o

should give you the same list as above.

Store the output of xclip in a variable and iterate over the programs calling
``which`` on each of them::

    $ req_progs=$(xclip -o)
    $ echo $req_progs
    xclip bowtie2 bowtie2-build velveth velvetg parallel samtools
    $ for p in $req_progs; do which $p || echo $p not in PATH; done
    /usr/bin/xclip
    /home/idb/bin/bowtie2
    /home/idb/bin/bowtie2-build
    /home/idb/downloaded_software/velvet_1.2.03/velveth
    /home/idb/downloaded_software/velvet_1.2.03/velvetg
    /usr/local/bin/parallel
    /home/idb/bin/samtools

As you can see all programs are found, except tablet in this case. If any of
the installed programs is missing, try to install them yourself or ask. If you
are having troubles following these examples, try to find some bash tutorials
online next time you have some time to kill. Educating yourself on how to use
the command line effectively increases your productivity immensely.

(Optional exercise) Check all programs in one go using xclip, parallel and which
================================================================================
The ``parallel`` program can be used to run something over multiple cores in
parallel. Try to rewrite the following statement, which prints the program name
twice, such that it prints the same output as in `Check all programs in one go
using xclip and which`_::
    
    $ xclip -o | parallel echo {} '&&' echo {}
    xclip
    xclip
    bowtie2
    bowtie2
    bowtie2-build
    bowtie2-build
    velveth
    velveth
    velvetg
    velvetg
    parallel
    parallel
    samtools
    samtools

Of course in this example making the statement execute in parallel is not that
exciting since the execution time is already extremely short. The execution
actually becomes slower than the original. This excercise is merely to gain
familiarity with the parallel syntax.

(Optional excercise) Install sickle by yourself
===============================================
Follow these steps only if you want to install ``sickle`` by yourself.
Installation procedures of research software often follow the same pattern.
Download the code, *compile* it and copy the binary to a location in your
``$PATH``. The code for sickle is on https://github.com/najoshi/sickle. I
prefer *compiling* my programs in ``~/src`` and then copying the resulting
program to my ``~/bin`` directory, which is in my ``$PATH``. This should get
you a long way::

    mkdir -p ~/src

    # Go to the source directory and clone the sickle repository
    cd ~/src
    git clone https://github.com/najoshi/sickle
    cd sickle

    # Compile the program
    make

    # Create a bin directory
    mkdir -p ~/bin
    cp sickle ~/bin
