---
layout: page
comments: true
title: pandoc
---

<https://pandoc.org/installing.html>

pandoc - это программа для конвертирования файлов. Например, .html в .md:

WIn+R cmd

```
cd desktop
pandoc 1.html -f html -t commonmark --wrap=preserve -o 1.md
```

Так что с этой программой ты можешь сохранить (Ctrl+S, только HTML) статью с какого-то сайта, [убрать](https://notepad-plus-plus.org/downloads/) всё лишнее из HTML и конвертировать его в MD, который ты можешь загрузить на [свой сайт](/ru/jekyll).