---
layout: post
title: Handy way to split MS Word files by page
---

I was looking for a way to create dynamically the files for [RePEc](https://ideas.repec.org/t/booktemplate.html)  for an academic journal starting from a CSV file.

I used MS Word mail merge function that generated a big file, each record (future .rdf file for RePEc) on a different page, separated by a page break. 

Next I needed to create one file for each of the records. 

After some google search I got to [this page](https://www.extendoffice.com/documents/word/966-word-split-documents-into-multiple-documents.html).

There are multiple solutions offered but I choose the one using some VBA code and steps (I reproduce them below just in case, but  you can also try the other versions, the MS Word plugin they suggest is pretty cool but you can use it for free for 60 days).

After the MS Word split, I used this tool [word2txt](http://www.download25.com/install/zilla-word-to-text-converter.html) to actually have text files out of them.

<script src="https://gist.github.com/czmole/eb70ff0f54053352ef466d5cfd9c8863.js"></script>