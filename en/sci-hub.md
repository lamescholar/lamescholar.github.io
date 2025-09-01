---
layout: page
comments: true
title: Sci-Hub
---

A script for downloading full magazine issues.
<br><br>

For the script to work, you need Python.

<https://www.python.org/downloads/>

When installing Python, you need to tick Add python.exe to PATH.
<br><br>

Here the script:

```
import argparse
import urllib.request

parser = argparse.ArgumentParser()
parser.add_argument('file', type=argparse.FileType('r'))
args = parser.parse_args()

i = 1
for x in args.file.readlines():
	url = "https://sci-hub.ru/" + x
	webUrl  = urllib.request.urlopen(url)
	html = webUrl.read()
	html = str(html)
	start = html.find('/downloads/')
	end = html.find('.pdf')
	pdfurl = "https://sci-hub.ru" + html[start:end+4]
	print(f"Downloading article {i}")
	urllib.request.urlretrieve(pdfurl, f"{i}.pdf")
	print("Done")
	i += 1
```

Create text file, insert code, close. Edit the name to scihub, the extension to .py.

Create cmd.txt. Insert:

```
cd "C:\Users\...\Sci-Hub"
python scihub.py DOI.txt
```

Create DOI.txt.

Put all 3 files into Sci-Hub folder

Open cmd.txt . "C:\Users\...\Sci-Hub" is the path to the Sci-Hub folder. PDF files will be uploaded to it.
<br><br>

Open DOI.txt . Fill it with links to articles.

Copy the contents of cmd.txt.

Win+R cmd Ctrl+V
<br><br>

Articles can be merged into one PDF file using the PDF-XChange Editor program.

<https://rutracker.org/forum/viewtopic.php?t=5998062>