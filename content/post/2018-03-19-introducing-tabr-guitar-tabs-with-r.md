---
title: 'Introducing tabr: guitar tabs with R'
author: Matthew Leonawicz
date: '2018-03-19'
slug: introducing-tabr-guitar-tabs-with-r
categories:
  - R
tags:
  - R package
  - tabr
  - sheet music
  - guitar
  - tablature
  - tabs
  - music notation
  - music transcription
  - LilyPond

header:
  caption: ''
  image: '../img/post/tabr_logo.png'
---

<p style="text-align:center;">
<img src="https://github.com/leonawicz/tabr/blob/master/data-raw/tabr_logo.png?raw=true" width="100%">
</p>

This post introduces a new R package I am working on called `tabr` for creating guitar tablature ("tabs") from R code. The `tabr` package provides programmatic music notation and a wrapper around [LilyPond](http://lilypond.org/) for creating quality guitar tablature.

`tabr` offers functions for describing and organizing musical structures and wraps around the LilyPond backend. LilyPond is an open source music engraving program for generating high quality sheet music based on markup syntax. `tabr` generates files following the LilyPond markup syntax to be subsequently processed by LilyPond into sheet music.

A standalone LilyPond (.ly) file can be created or the package can make a system call to LilyPond directly to render the guitar tablature output (pdf or png). While LilyPond caters to sheet music in general, `tabr` is focused on leveraging it specifically for creating quality guitar tablature.

While music can be quite complex and a full score will be much longer, something as simple as the following code snippet produces the music notation in the accompanying image.

``` r
p("r a2 c f d a f c4", "4 8*6 1") %>% track %>% score %>% tab("out.pdf")
```

<p style="text-align:center;">
<img src="https://github.com/leonawicz/tabr/blob/master/data-raw/staff_with_code.png?raw=true" width="100%">
</p>

Installation
------------

You can install tabr from GitHub with:

``` r
# install.packages('devtools')
devtools::install_github("leonawicz/tabr")
```

Basic example
-------------

As a brief example, recreate the tablature shown in the `tabr` logo, which is almost the same as the first measure in the code example above. It has a tiny bit more in the form of metadata and doesn't take as many shortcuts, but it's still short. Here are the steps.

-   Define a musical phrase with `phrase` or the shorthand alias `p`.
-   Add the phrase to a `track`.
-   Add the track to a `score`.
-   Render the score to pdf with `tab`.

Constructing a musical phrase
-----------------------------

A phrase here does not require a strict definition. Think of it as the smallest piece of musical structure you intend to string together. The first argument to `phrase` is a string describing notes of a specific pitch (or rests: "r"), separated in time by spaces. For chords, just remove spaces to indicate simultaneous notes. Integers are appended to indicate the octave number so that the pitch is unique. For example, a rest followed by a sequence of notes might be given by `notes = "r a2 c3 f3 d3 a3 f3"`.

The second argument is a similar string giving note metadata. In this example there is nothing to add but the time durations. Whole notes taking up an entire measure of music are given by 1, half notes by 2, quarter notes 4, eighth notes 8, and so on. To specify a quarter note rest followed by a sequence of eighth notes, use `info = "4 8 8 8 8 8 8"`. This basic example does not require specifying additional note information such as dotted notes for different fractions of time, staccato notes, ties/slurs, slides, bends, hammer ons and pull offs, etc. These specifications are currently available in `tabr` to varying degrees of development and are covered in the vignette tutorials.

The third argument, `string`, is optional but generally important for guitar tablature. In similar format, it specifies the strings of the guitar on which notes are played. Providing this information fixes the fret-string combinations so that LilyPond does not have to guess what position on the neck of the guitar to play a specific note. An inability to specify this in various tablature notation software (or laziness by the user), is a common cause of inaccurate tabs scouring the internet, where even when the notes are correct they are written in the tab suggesting they be played in positions no one would sensibly use. Note that the `x` shown below is just a placeholder indicating no need to specify a string for the quarter note rest.

Score metadata and accessing LilyPond
-------------------------------------

Finally, specify some song metadata to reproduce the original staff: the key of D minor, common time, and the tempo. If LilyPond is installed on your system (and added to your system PATH variable on Windows systems), `tab` should call it successfully. Alternatively, on Windows, it can be added explicitly by calling `tabr_options`. This option to specify the LilyPond path is still available on other systems. An example of this is commented out below.

R code
------

``` r
library(tabr)
# path <- 'C:/Program Files (x86)/LilyPond/usr/bin/lilypond.exe'
# tabr_options(lilypond = path)

p1 <- p("r a2 c3 f3 d3 a3 f3", "4 8 8 8 8 8 8", "x 5 5 4 4 3 4")
track1 <- track(p1)
song <- score(track1)
tab(song, "phrase.pdf", key = "dm", time = "4/4", tempo = "4 = 120")
```

    #> #### Engraving score to phrase.pdf ####
    #> GNU LilyPond 2.18.2
    #> Processing `./phrase.ly'
    #> Parsing...
    #> Interpreting music...
    #> Preprocessing graphical objects...
    #> Interpreting music...
    #> MIDI output to `./phrase.mid'...
    #> Finding the ideal number of pages...
    #> Fitting music on 1 page...
    #> Drawing systems...
    #> Layout output to `./phrase.ps'...
    #> Converting to `./phrase.pdf'...
    #> Success: compilation successfully completed

See the pdf result embedded at the [tabr website](https://leonawicz.github.io/tabr/).

Development status, context and caveats
---------------------------------------

First, why LilyPond? LilyPond is an exceptional sheet music engraving program. It produces professional, high quality output. It is open source. It offers an access point for a programmatic approach to music notation. It is developed and utilized by a large community. Most GUI-based applications are WYSIWYG and force a greater limitation on what you can do and what it will look like after you do it. On the other hand, I have zero interest in writing LilyPond files. `tabr` has made it more enjoyable, a bit less ugly, and enables me to stick with LilyPond for its quality as I try to shield myself from its native input structures. I'm sure there are far more LilyPond users who don't mind it at all and have never heard of R; to each their own.

The `tabr` package is in early development. Breaking changes could occur in a later version. Many capabilities are missing. Others are incompletely implemented. Others in the R developer community who are probably much better musicians than myself are welcome to contribute. This is the type of package that will only develop in response to specific needs of its contributor(s). There are many things that `tabr` does not address at this stage of development. For example, `tabr` assumes standard guitar tuning. It has no ability to recognize or handle non-standard tunings or instruments like bass with a different number of strings. There are essentially countless other aspects of music notation available in LilyPond that `tabr` does not wrap around. The aim is not to do it all, but certainly to do much more than is currently in place.

I am not an expert in music theory, or in music notation and transcription, or in LilyPond. In fact, my skill in music notation is ironically low enough that I do not find it any more challenging or an impediment to describe a song in R code rather than to just tab it out by hand. The main intent with `tabr`, however, is simply to be able to generate markup files that LilyPond accepts and understands, without having to write that markup directly.

Finally, there are nonetheless limitations to LilyPond itself. It has been developed for sheet music in general and guitar tablature features were added as a relative afterthought. There are plenty of features I have not yet developed R wrappers around. Then there are other features like string bending that are technically available, but not fully developed yet on the LilyPond side either. Case in point, LilyPond's bend engraver is still under development; specifying something as common as a bend-release-pull-off is, to put it mildly, challenging.

Reference
---------

[Complete package reference and function documentation](https://leonawicz.github.io/tabr/)
