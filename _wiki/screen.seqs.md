---
title: 'screen.seqs'
tags: 'commands'
redirect_from: '/wiki/Screen.seqs.html'
---
The **screen.seqs** command enables you to keep
sequences that fulfill certain user defined criteria. Furthermore, it
enables you to cull those sequences not meeting the criteria from a
names, group, contigsreport, alignreport and summary file. As an
example, we will use the example from the [Sogin data
analysis](/wiki/sogin_data_analysis) example.

## Default settings

First, we can get a summary of the characteristics of the unaligned or
aligned sequences:

    mothur > summary.seqs(fasta=sogin.unique.align)

           Start   End NBases  Ambigs  Polymer
    Minimum:   109 222 40  0   2
    2.5%-tile: 4648    4875    57  0   3
    25%-tile:  4655    4928    60  0   3
    Median:    4655    4928    62  0   4
    75%-tile:  4655    4928    65  0   4
    97.5%-tile:    4655    4939    73  0   6
    Maximum:   6793    6850    100 0   31
    # of Seqs: 21907

You will be able to screen for each of these characteristics using the
start, end, maxambig, maxhomop, minlength, and maxlength options. Any of
these options can be combined in a single command. Problematic sequence
names can also be removed from the name and group files with the name,
and group options.

## Options

### start & end

You may have noticed that when you make an alignment there are some
sequences that do not align in the same region as most of the sequences
that you are analyzing. For example, in the Sogin dataset, there was at
least one sequence whose alignment started at position 109 and a
sequence that ended by position 222 while most sequences started by 4655
and ended by position 4928. The following command will remove sequences
that start after position 4655:

    mothur > screen.seqs(fasta=sogin.unique.align, start=4655)

To remove the sequences that end before position 4928, the following
command will work:

    mothur > screen.seqs(fasta=sogin.unique.align, end=4928)

Putting it all together the following command will remove those
sequences that don't start by position 4655 and do end before position
4928:

    mothur > screen.seqs(fasta=sogin.unique.align, start=4655, end=4928)
    mothur > summary.seqs(fasta=sogin.unique.good.align)

           Start   End NBases  Ambigs  Polymer
    Minimum:   4615    4928    50  0   2
    2.5%-tile: 4652    4928    57  0   3
    25%-tile:  4655    4928    60  0   3
    Median:    4655    4928    62  0   4
    75%-tile:  4655    4928    65  0   4
    97.5%-tile:    4655    4938    72  0   6
    Maximum:   4655    5014    100 0   31
    # of Seqs: 20670

### minlength & maxlength

In some studies an investigator may get a bunch of 5' sequences and
some full length sequences, in others an investigator might want to make
sure that pyrosequences are within some window for length as a quality
control measure. As an example, the Sogin data set had 16S rRNA V6
pyrosequences ranging in length between 40 and 100 bp. To remove
sequences shorter than 50 bp, the minlength option should be used:

    mothur > screen.seqs(fasta=sogin.unique.align, minlength=50)

Alternatively, to remove sequences longer than 70 bp, the maxlength
option should be used:

    mothur > screen.seqs(fasta=sogin.unique.align, maxlength=70)

Putting it together to keep only those sequences that are between 50 and
70 bp:

    mothur > screen.seqs(fasta=sogin.unique.align, minlength=50, maxlength=70)
    mothur > summary.seqs(fasta=sogin.unique.good.align)

           Start   End NBases  Ambigs  Polymer
    Minimum:   109 222 50  0   2
    2.5%-tile: 4648    4875    57  0   3
    25%-tile:  4655    4928    60  0   3
    Median:    4655    4928    62  0   4
    75%-tile:  4655    4928    64  0   4
    97.5%-tile:    4655    4939    69  0   6
    Maximum:   6785    6850    70  0   9
    # of Seqs: 20160

### maxambig

As part of their initial screening procedure, Sogin and colleagues
removed any sequences with any ambiguous bases. You can do this with the
maxambig option:

    mothur > screen.seqs(fasta=sogin.unique.align, maxambig=0)

### maxn

The maxn parameter has the same function as maxambig. It is retained as
a separate command to avoid problems for users running scripts developed
on older versions of the program. As a sequence is read in, any
degenerate bases are converted to 'N's.

### maxhomop

While we don't necessarily know the longest acceptable homopolymer for
a 16S rRNA gene, the max length of 31 is clearly a sequencing artifact.
If you are interested in removing sequences with excessively long
homopolymers, then you should use the maxhomop option:

    mothur > screen.seqs(fasta=sogin.unique.align, maxhomop=8)
    mothur > summary.seqs(fasta=sogin.unique.good.align)

           Start   End NBases  Ambigs  Polymer
    Minimum:   109 222 40  0   2
    2.5%-tile: 4648    4875    57  0   3
    25%-tile:  4655    4928    60  0   3
    Median:    4655    4928    62  0   4
    75%-tile:  4655    4928    65  0   4
    97.5%-tile:    4655    4939    73  0   6
    Maximum:   6793    6850    100 0   8
    # of Seqs: 21896

### group, name, count, qfile, taxonomy

If you apply **screen.seqs** as we have in the previous sections and then
attempt to run any downstream commands that need a name, group, qfile,
count and taxnomy file, the files will be incompatible since those files
will still contain information for sequences that you culled. To get
around this you can use the group and name option:

    mothur > screen.seqs(fasta=sogin.unique.align, start=4655, end=4928, maxhomop=6, name=sogin.names, group=sogin.groups, qfile=sogin.qual, alignreport=sogin.unique.align.report, taxonomy=sogin.unique.rdp.taxonomy)
    mothur > summary.seqs(fasta=sogin.unique.good.align)

           Start   End NBases  Ambigs  Polymer
    Minimum:   4615    4928    50  0   2
    2.5%-tile: 4652    4928    57  0   3
    25%-tile:  4655    4928    60  0   3
    Median:    4655    4928    62  0   4
    75%-tile:  4655    4928    65  0   4
    97.5%-tile:    4655    4938    72  0   6
    Maximum:   4655    5014    100 0   6
    # of Seqs: 20530

Looking at the sogin.good.name files and
sogin.good.unique.good.align.report files we see that there are now
20,530 entries representing a total of 216,243 sequences, which agrees
with sogin.unique.good.align. Next, looking at sogin.good.groups we see
that there are a total of 216,243 sequences, which also agrees.

or with a [ count file](/wiki/Count_File)

    mothur > screen.seqs(fasta=sogin.unique.align, start=4655, end=4928, maxhomop=6, count=sogin.count_table, qfile=sogin.qual, alignreport=sogin.unique.align.report, taxonomy=sogin.unique.rdp.taxonomy)

### optimize && criteria

The optimize and criteria parameters allow you set the start, end,
maxabig, maxhomop, minlength, maxlength, minoverlap, ostart, oend,
mismatches, maxn, minscore, maxinsert and minsim parameters relative to
your set of sequences. The following command would remove all sequences
that started after the position that 90% of the sequences do.

    mothur > screen.seqs(fasta=sogin.unique.align, optimize=start, criteria=90) 

Using the optimize parameter trumps the value given for the start
parameter if you have provided it. You can optimize to several
parameters by separating by dashes. Example:
optimize=start-end-minlength, would remove any sequence that starts
after the position that 90% of the sequences do, or ends before the
position that 90% of the sequences do, or whose length is shorter than
90% of the sequences.

### summary

The summary file allows you to enter the summary file created by
[summary.seqs](/wiki/summary.seqs) to save processing time when
screening with parameters in the summary file. The parameters in the
summary file are: start, end, maxambig, maxhomop, minlength and
maxlength.

    mothur > summary.seqs(fasta=sogin.unique.align)
    mothur > screen.seqs(fasta=sogin.unique.align, summary=sogin.unique.summary, minlength=50, maxlength=70)

### contigsreport

The contigs report file is created by the
[make.contigs](/wiki/make.contigs) command. If you provide the
contigs report file you can screen your sequences using the following
parameters: minoverlap, ostart, oend and mismatches.

#### minoverlap

The minoverlap parameter is used to set a minimum overlap length. It can
only be used with a contigsreport file.

    mothur > screen.seqs(fasta=stability.trim.contigs.fasta, contigsreport=stability.trim.contigs.report, minoverlap=25)

#### ostart && oend

The ostart and oend parameters are similar to the start and end
parameters. Setting the ostart parameter sets a position the overlap
must start by. Setting the oend parameter sets a position the overlap
must end after. They can only be used with a contigsreport file.

#### mismatches

The mismatches parameter allows you to set and maximum mismatches in the
\*.contigs.report.

    mothur > screen.seqs(fasta=stability.trim.contigs.fasta, contigsreport=stability.trim.contigs.report, mismatches=5)

### alignreport

The align report file is created by the
[align.seqs](/wiki/align.seqs) command. If you provide the align
report file you can screen your sequences using the following
parameters: minscore, maxinsert and minsim.

#### minscore

The minscore parameter allows you to set the minimum search score during
alignment. Found in column 'SearchScore' in align.report file.

#### maxinsert

The maxinsert parameter allows you to set the maximum number of
insertions during alignment. Found in column 'LongestInsert' in
align.report file.

#### minsim

The minsim parameter allows you to set the minimum similarity to
template sequences during alignment. Found in column
'SimBtwnQuery&Template' in align.report file.

### processors

The processors parameter allows you to run the command with multiple
processors. Default processors=Autodetect number of available processors
and use all available.

    mothur > screen.seqs(fasta=sogin.unique.align, start=4655, end=4928, maxhomop=6, name=sogin.names, group=sogin.groups, alignreport=sogin.unique.align.report, processors=2)

## Revisions

-   1.23.0 Added taxonomy parameter
-   1.24.0 Paralellized for Windows.
-   1.28.0 Added count parameter
-   1.30.0 Added contigsreport, alignreport and summary files to allow
    files to be screened using their inputs. added minoverlap, ostart,
    oend, mismatches, maxn, minscore, maxinsert, minsim parameters and
    optimization types of minoverlap, ostart, oend, mismatches, maxn,
    minscore, maxinsert, minsim.
-   1.32.0 Bug Fix: for count tables without group information, mothur
    was not creating the \*good.count\_table correctly. Which could
    cause fasta/count file mismatch errors downstream.
-   1.32.0 Allowed for percent in the criteria parameter.
-   Changes minlength default to 10.
    [\#160](https://github.com/mothur/mothur/issues/160)
-   1.39.0 Fixes bug with optimize parameter using alignreport file
-   1.40.0 Reduces memory usage
    [\#319](https://github.com/mothur/mothur/issues/319)
-   1.40.0 Rewrite of threaded code. Default processors=Autodetect
    number of available processors and use all available.
-   1.40.4 - Bug Fix: pcr.seqs and **screen.seqs** (with no bad reads
    detected), causing accnos file issue.
-   1.40.5 - Bug Fix: not making \*good.groups or \*good.count\_table
    files. [\#476](https://github.com/mothur/mothur/issues/476)


