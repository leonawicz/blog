---
title: tabr package for guitar tablature now on CRAN
author: Matthew Leonawicz
date: '2018-04-19'
slug: tabr-package-for-guitar-tablature-now-on-cran
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
  image: '../img/post/tabr.png'
---

<p style="text-align:center;">
<a href="https://github.com/leonawicz/tabr"><img src="https://github.com/leonawicz/tabr/blob/master/data-raw/tabr.png?raw=true" width="40%"></a>
</p>

The [tabr](https://github.com/leonawicz/tabr) package for creating guitar tablature ("tabs") from R code is now available on CRAN. `tabr` provides programmatic music notation and a wrapper around [LilyPond](http://lilypond.org/) for creating quality guitar tablature.

`tabr` offers functions for describing and organizing musical structures and wraps around the LilyPond backend. LilyPond is an open source music engraving program for generating high quality sheet music based on markup syntax. `tabr` generates files following the LilyPond markup syntax to be subsequently processed by LilyPond into sheet music.

A standalone LilyPond (.ly) file can be created or the package can make a system call to LilyPond directly to render the guitar tablature output (pdf or png). While LilyPond caters to sheet music in general, `tabr` is focused on leveraging it specifically for creating quality guitar tablature.

While music can be quite complex and a full score will be much longer, something as simple as the following code snippet produces the music notation in the accompanying image.

``` r
p("r a2 c f d a f c4", "4 8*6 1") %>% track %>% score %>% tab("out.pdf")
```

<p style="text-align:center;">
<img src="https://github.com/leonawicz/tabr/blob/master/data-raw/staff_with_code.png?raw=true" width="100%">
</p>

Functionality and support
-------------------------

The `tabr` package offers the following:

* Render guitar tablature and sheet music to pdf or png.
* Write accompanying MIDI files that can respect repeat notation and transposition in the sheet music (under reasonable conditions).
* Support tablature for other string instruments besides guitar such as bass or banjo.
* Support for instruments with different numbers of strings.
* Support for arbitrary instrument tuning.
* Offers inclusion (or exclusion) of formal music staves above tab staves, such as treble and bass clef staves for complete rhythm and timing information.
* Track-specific setup for features like instrument type, tuning and supplemental music staves.
* Provide common notation such as slide, bend, hammer on, pull off, slur, tie, staccato, dotted notes, visible and silent rests.
* Allows arbitrary tuplet structure.
* Above-staff text annotation.
* Percent and volta repeat section notation.
* Note transposition.
* Staff transposition.
* Multiple voices per track and multiple tracks per score.
* Chord symbols above staff
* Chord fretboard diagrams and chord chart at top of score.
* Rich set of layout control options covering settings from score attributions to font size.
* Optional alternative input format allowing the user to provide string/fret combinations (along with key signature and instrument tuning) to map to pitch.

Note that MIDI support and string/fret alternative input format support are not prioritized in ongoing `tabr` development. These are considered tangential extra features in `tabr` that fall outside the general scope and intent of the package.

Basic example
-------------

A brief example below highlights the general workflow.

-   Define a musical phrase with `phrase` or the shorthand alias `p`.
-   Add the phrase to a `track`.
-   Add the track to a `score`.
-   Render the score to pdf with `tab`.

Constructing a musical phrase
-----------------------------

A phrase here does not require a strict definition. Think of it as the smallest piece of musical structure you intend to string together. The first argument to `phrase` is a string describing notes of a specific pitch (or rests: "r"), separated in time by spaces. For chords, just remove spaces to indicate simultaneous notes. Integers are appended to indicate the octave number so that the pitch is unique. For example, a rest followed by a sequence of notes might be given by `notes = "r a2 c3 f3 d3 a3 f3"`.

The second argument is a similar string giving note metadata. In this example there is nothing to add but the time durations. Whole notes taking up an entire measure of music are given by 1, half notes by 2, quarter notes 4, eighth notes 8, and so on. To specify a quarter note rest followed by a sequence of eighth notes, use `info = "4 8 8 8 8 8 8"`. This basic example does not require specifying additional note information such as dotted notes for different fractions of time, staccato notes, ties/slurs, slides, bends, hammer ons and pull offs, etc. These specifications are currently available in `tabr` to varying degrees of development and are covered in the vignette tutorials.

The third argument, `string`, is optional but generally important for guitar tablature. In similar format, it specifies the strings of the guitar on which notes are played. Providing this information fixes the fret-string combinations so that LilyPond does not have to guess what position on the neck of the guitar to play a specific note. An inability to specify this in various tablature notation software (or laziness by the user), is a common cause of inaccurate tabs scouring the internet, where even when the notes are correct they are written in the tab suggesting they be played in positions no one would sensibly use. Note that the `x` shown below is just a placeholder indicating no need to specify a string for the quarter note rest.

The example below employs a couple shortcuts to further reduce typing, using the `*` in-string expansion operator to avoid typing a long series of eighth notes. It also drops explicit reference to octave number three since this central octave is the default octave in LilyPond. While explicit string numbers are not needed for this example, they are provided anyway for full context.

Score metadata and accessing LilyPond
-------------------------------------

Finally, specify some song metadata to reproduce the original staff: the key of D minor, common time, and the tempo.

If LilyPond is installed on your system (and added to your system PATH variable on Windows systems), `tab` should call it successfully. Alternatively, on Windows, it can be added explicitly by calling `tabr_options`. This option to specify the LilyPond path is still available on other systems. An example of this is commented out below. However, `tabr` will do its best on package load to set these paths in `tabr_options` for you if it can successfully detect a LilyPond installation in a standard file system location, so you may not have to do anything.

R code
------

``` r
library(tabr)
# path <- 'C:/Program Files (x86)/LilyPond/usr/bin/lilypond.exe'
# tabr_options(lilypond = path)

p1 <- p("r a2 c f d a f", "4 8*6", "x 5 5 4 4 3 4")
song <- p1 %>% track %>% score
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

Additional context
-----------------

Why LilyPond? LilyPond is an exceptional sheet music engraving program. It produces professional, high quality output. It is open source. It offers an access point for a programmatic approach to music notation. It is developed and utilized by a large community. Most GUI-based applications are WYSIWYG and force a greater limitation on what you can do and what it will look like after you do it. On the other hand, I have zero interest in writing LilyPond files. `tabr` has made it more enjoyable, a bit less ugly, and enables me to stick with LilyPond for its quality as I try to shield myself from its native input structures. I'm sure there are far more LilyPond users who don't mind it at all and have never heard of R; to each their own.

Limitations
-----------

There is far more that LilyPond can do that `tabr` does not tap into. Instead of listing a million things, this is just to highlight an example of a critical feature that still has limited functionality in both `tabr` and in LilyPond itself: LilyPond's bend engraver. Rendering sheet music with quality string bend notation is quite difficult. This is an area that will benefit greatly from further development.

Reference
---------

There is a rich collection of vignette tutorials available at the tabr website.

[Complete package reference and function documentation](https://leonawicz.github.io/tabr/)
