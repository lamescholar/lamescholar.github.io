---
layout: page
comments: true
title: pandoc
---

<https://pandoc.org/installing.html>

pandoc is a program to convert files. For example, it can covert .html to .md:

Win+R cmd

```
cd desktop
pandoc 1.html -f html -t commonmark --wrap=preserve -o 1.md
```

So with this program you can save (Ctrl+S, only HTML) an article from some site, [remove](https://notepad-plus-plus.org/downloads/) everything extra from HTML and convert it to MD, which you can upload on [your site](/en/jekyll).