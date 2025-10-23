---
layout: page
comments: true
title: OCR
---

Here I list programs that can get the text out of the screenshot.
<br><br>

ABBYY Screenshot Reader - <https://btdig.com/dfe064427884e2190cd2d8c93f4cc9ce6d26f301/abbyy-finereader-kpojiuk>
<br><br>

ABBYY Screenshot Reader not always work properly. For example, it works poorly with old German fonts or any wiggly font. Tesseract manages it better.
<br><br>

Tesseract:

<https://github.com/UB-Mannheim/tesseract/wiki>

<https://tesseract-ocr.github.io/tessdoc/Command-Line-Usage.html>

Install Tesseract with all language additions. Add installation folder to PATH.

Now, suppose you got screenshot of German text on Desktop - 1.jpg. Or you may do a crop with IrfanView. Ctrl+Y, S.

Usage:

Win+R cmd

```
cd desktop
tesseract 1.jpg - -l deu
```

You get the text right in the сommand line.
<br><br>

Capture2Text - <https://capture2text.sourceforge.net/>

Point a mouse at the corner of the text. Win+Q. Draw a rectangle. Text is recognized into buffer.

Disable WIn+R shotcut.

Program use Tesseract for recognition. Training data is out of date - 2015. You need to replace it. Delete tessdata folder. Copy and paste tessdata folder from Tesseract installation folder.

<https://github.com/UB-Mannheim/tesseract/wiki>