From text to talk (ACL2022)
================
Mark Dingemanse & Andreas Liesenfeld
2022-03-20

> **Abstract:** Informal social interaction is the primordial home of
> human language. Linguistically diverse conversational corpora are an
> important and largely untapped resource for computational linguistics
> and language technology. Through the efforts of a worldwide language
> documentation movement, such corpora are increasingly becoming
> available. We show how interactional data from 63 languages (26
> families) harbours insights about turn-taking, timing, sequential
> structure and social action, with implications for language
> technology, natural language understanding, and the design of
> conversational interfaces. Harnessing linguistically diverse
> conversational corpora will provide the empirical foundations for
> flexible, localizable, humane language technologies of the future.

# Introduction

This document produces the figures and analyses reported in the ACL2022
paper “From text to talk: Harnessing conversational corpora for humane
and diversity-aware language technology”.

The paper is based on a curated collection of conversational corpora
that are individually made available for research purposes. The full set
of 0 corpora for 73 of 29 is documented in a separate code notebook,
along with reports on the most important features of each corpus.

Not all of the languages or corpora are represented in all analyses and
figures presented in the paper, because the corpora differ in size,
precision of annotation, level of transcription. Accounts of inclusions
and exclusions are provided in the [reports by
language](./1_reports.md).

**Note on data availability.** The corpora we rely on are made available
for research purposes, but come under a variety of usage restrictions
which in many cases (and for sensible reasons) prevent redistribution.
We try to provide all relevant details about the corpora and how to
access them in the following ways:

1.  All corpora are cited in the paper with at least the name of the
    compilers and a durable HANDLE or DOI locator.
2.  Links to all corpora and a considerable amount of additional data
    are also provided in the separate [reports by
    language](./1_reports.md).
3.  Our data curation workflow is detailed in [this
    preprint](https://doi.org/10.48550/arXiv.2203.03399).

This also means that the report below is based on the full data but we
cannot share all of this data in the repository. Instead, we can share
only derived measures and samples. We have tried to make our analysis as
perspicuous as possible by including the code used to generate the
measures and samples in the [Rmd code](./2_analyses.Rmd).

# Data overview and map

The subset of corpora considered here amounts to around 800 hours of
speech, or 9.3 million words, segmented into 1.6 million annotations
produced by over 11.000 participants.

    ## # A tibble: 63 x 6
    ##    language       turns  words minutes  hours people
    ##    <chr>          <int>  <dbl>   <dbl>  <dbl>  <int>
    ##  1 +Akhoe           721   3253    28.7  0.478     18
    ##  2 Akpes            635   3965    17.8  0.296      4
    ##  3 Ambel           1509   6601    42.0  0.700     22
    ##  4 Anal            6767  26826   278.   4.63      54
    ##  5 Arabic         33120 201207  1211.  20.2      365
    ##  6 Arapaho         4821  55850   243.   4.06     109
    ##  7 Baa             1361  12553    65.3  1.09       7
    ##  8 Br. Portuguese  3242  17109    88.4  1.47       2
    ##  9 Catalan        11059  93827   398.   6.64      83
    ## 10 Chitkuli        1123  13462    68.3  1.14      20
    ## # ... with 53 more rows

We generate a map with numbers for labels (used in the paper).

![](2_analyses_files/figure-gfm/ACL_map-1.png)<!-- -->

We also produce a graph of language resources by size.

![](2_analyses_files/figure-gfm/language_resources-1.png)<!-- -->

# Turn-taking & timing

We look at the timing of turn-taking in sufficiently large corpora,
limiting the analysis to dyadic interactions because triadic and
multi-party interaction is qualitatively different. We determine
participation framework based on a 10 second rolling window: if in the
window there are no more than 2 participants we count the interaction at
that point as dyadic.

Five corpora are excluded from these analyses because they have unclear
or incommensurable segmentation conventions: Brazilian Portuguese,
Croatian, Czech, Hungarian, and Nganasan. A further number of corpora do
not feature at least 1000 dyadic turn transitions.

There are 24 languages of 1 language families in which the corpora
provide &gt;1000 turn transitions in dyadic settings. The median floor
transfer onset time (FTO) across the sample is 10 ms, very close to the
no-gap no-overlap goal seen in prior work.

![](2_analyses_files/figure-gfm/turntaking_plot-1.png)<!-- -->

# Unity and diversity

As a language-agnostic approach to activity types, we consider a
distinction between ‘chats’ and ‘chunks’. We identify a number of these
and plot them in six unrelated languages. Chunks are identified by
looking for streaks of &gt;2 identical turns by the same participant
occurring in close succession while they make up less than 30% of talk
in the surrounding 10 second window.

Chats are identified by looking for turns with a duration of 3 seconds
that occur in a regime where contributions in the 10 second window
surrounding them are evenly distributed (both speakers contribution
between 40% to 60% of talk).

![](2_analyses_files/figure-gfm/chats-1.png)<!-- -->

We find that the most frequent turn formats used in English and Korean
tellings are ‘mhm’ and ‘eung’ respectively. We plot 4 examples of 80
second stretches featuring continuers, and sample 100 such segments for
each of the languages to compare the relative frequency of continuers.

We sample 100 stretches of 80000 ms (80 s) in each of the languages.

The sample is randomized each time, but with the seed used in the paper,
we end up with 100 samples from 53 Korean source recordings with 106
distinct participants, and another 100 samples from 55 English source
recordings with 96 distinct participants.

Here are the basic descriptive statistics for number of total turns,
mean number of continuers, and overlap.

    ## # A tibble: 2 x 9
    ##   langshort n_turns mean_cont n_cont_sd mean_rel n_rel_sd mean_inv n_inv_sd
    ##   <chr>       <dbl>     <dbl>     <dbl>    <dbl>    <dbl>    <dbl>    <dbl>
    ## 1 English      30.5      2.56      1.71   0.0920   0.0859    14.5     12.8 
    ## 2 Korean       35.7      6.98      4.22   0.201    0.103      6.99     4.95
    ## # ... with 1 more variable: mean_overlap <dbl>

Note that average duration and number of turns per 10 second window is
not very different across the two languages, so won’t really explain
this:

    ## # A tibble: 2 x 4
    ##   language meanduration turnsper10sec wordsperturn
    ##   <chr>           <dbl>         <dbl>        <dbl>
    ## 1 english         1871.          5.64         6.85
    ## 2 korean          2545.          5.55         5.74

Putting it all together, we get at the following figure:

![](2_analyses_files/figure-gfm/contfreq_fig-1.png)<!-- -->

# Interactional tools

The number of truly unique turns across the whole dataset is 1096474.
However, the total number of turns is 1532886, so at least a quarter
across all languages (436412 out of 1532886) occurs more than once. Of
these, one fifth (329634) occur more than 20 times.

For analysing the relation between frequency and rank at the level of
turn formats we use only corpora in which there are at least 20
recurring turn formats. There are 22 such languages (representing 8
families). We also look at a further set of 17 smaller corpora
(representing 21 languages of 18 families) in which there at least 9
recurring turn formats.

![](2_analyses_files/figure-gfm/zipf2-1.png)<!-- -->

## Recurrent turn formats

What is the proportion of multiword versus one word recurrent turn
formats?

    ## # A tibble: 2 x 3
    ##   words     n  prop
    ##   <chr> <int> <dbl>
    ## 1 more    225   0.4
    ## 2 one     370   0.6

# Appendices

## Validation of turn-taking measures

Stivers et al. 2009 work with polar questions only. We can try to
approach that by looking at all FTOs of turn types that are reasonably
frequent (= likely to be conventionalized responses to polar questions)
that follow turns that end in a question mark.

We limit ourselves to languages in which 250 such sequences are found.
Here are, for each of these 10 languages, one example of a candidate QA
sequence so identified:

<table>
<thead>
<tr>
<th style="text-align:left;">
language
</th>
<th style="text-align:left;">
Q
</th>
<th style="text-align:left;">
A
</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:left;">
Catalan
</td>
<td style="text-align:left;">
a quina hora li he dit que arribava?
</td>
<td style="text-align:left;">
sí
</td>
</tr>
<tr>
<td style="text-align:left;">
Dutch
</td>
<td style="text-align:left;">
maar een zomerjurk?
</td>
<td style="text-align:left;">
ja
</td>
</tr>
<tr>
<td style="text-align:left;">
English
</td>
<td style="text-align:left;">
thats going to your house right?
</td>
<td style="text-align:left;">
yeah
</td>
</tr>
<tr>
<td style="text-align:left;">
German
</td>
<td style="text-align:left;">
und äh wir waren jetzt ja äh äh soll ich dir mal alles der Reihe nach
erzählen?
</td>
<td style="text-align:left;">
ja
</td>
</tr>
<tr>
<td style="text-align:left;">
Kerinci
</td>
<td style="text-align:left;">
lebih baik itòh bé jadi maharnyo kan?
</td>
<td style="text-align:left;">
iyò
</td>
</tr>
<tr>
<td style="text-align:left;">
Korean
</td>
<td style="text-align:left;">
ja-gi-do geu teum-e ggi-eo-seo gan geo-ya?
</td>
<td style="text-align:left;">
eung
</td>
</tr>
<tr>
<td style="text-align:left;">
Mandarin
</td>
<td style="text-align:left;">
hao de hao de hao de hao jiu zhege shiqing shiba?
</td>
<td style="text-align:left;">
e
</td>
</tr>
<tr>
<td style="text-align:left;">
Polish
</td>
<td style="text-align:left;">
a czy znala jezyk litewski?
</td>
<td style="text-align:left;">
mhm
</td>
</tr>
<tr>
<td style="text-align:left;">
Sambas
</td>
<td style="text-align:left;">
itoq lah anak béduwaq i?
</td>
<td style="text-align:left;">
eeq
</td>
</tr>
<tr>
<td style="text-align:left;">
Spanish
</td>
<td style="text-align:left;">
oye y la estela cómo está?
</td>
<td style="text-align:left;">
sí
</td>
</tr>
</tbody>
</table>

Then we print the number of candidate QA sequences by language and plot
the distribution of FTOs (floor transfer onset times).

    ## # A tibble: 10 x 2
    ##    language     n
    ##    <chr>    <int>
    ##  1 Catalan    930
    ##  2 Dutch      557
    ##  3 English   1230
    ##  4 German    1540
    ##  5 Kerinci    682
    ##  6 Korean    4294
    ##  7 Mandarin  2698
    ##  8 Polish     685
    ##  9 Sambas     501
    ## 10 Spanish   2363

![](2_analyses_files/figure-gfm/qa_plot-1.png)<!-- -->

## Power law plots for smaller corpora

While the body of the paper provides a plot for 22 large corpora, here
we als plot the rank-frequency distributions for turns and words for 21
smaller corpora in which there are at least 9 recurrent turn formats.

![](2_analyses_files/figure-gfm/zipf_sup-1.png)<!-- -->

## Table of language data

This table shows language name, family, glottocode and citation key. The
paper contains full bibliographic metadata.

    ## # A tibble: 63 x 4
    ##    Language       Family         glottocode Citation                            
    ##    <chr>          <chr>          <chr>      <chr>                               
    ##  1 +Akhoe         Khoe-Kwadi     haio1238   widlokCollectionAkhoeHai2007        
    ##  2 Akpes          Atlantic-Congo akpe1248   lauDocumentingAbesabesi2019         
    ##  3 Ambel          Austronesian   waig1244   arnoldDocumentationAmbelAustronesia~
    ##  4 Anal           Sino-Tibetan   anal1239   ozerovCommunitydrivenDocumentationN~
    ##  5 Arabic         Afro-Asiatic   egyp1253   canavanalexandraCALLHOMEEgyptianAra~
    ##  6 Arapaho        Algic          arap1274   cowellConversationalDatabaseArapaho~
    ##  7 Baa            Atlantic-Congo kwaa1262   mollernwadigoDocumentationProjectBa~
    ##  8 Br. Portuguese Indo-European  braz1246   dasilvaProjetoNormaUrbana1996       
    ##  9 Catalan        Indo-European  stan1289   garridoGlissandoCorpusMultidiscipli~
    ## 10 Chitkuli       Sino-Tibetan   chit1279   martinezDocumentaryCorpusChhitkulRa~
    ## # ... with 53 more rows
