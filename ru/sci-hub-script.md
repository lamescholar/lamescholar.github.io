---
layout: page
comments: true
title: Sci-Hub
---

Скрипт для скачивания номеров журналов целиком.
<br><br>

Для работы скрипта необходим Python.

<https://www.python.org/downloads/>

При установке Python нужно поставить галочку Add python.exe to PATH.
<br><br>

Вот сам скрипт:

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

Создаёшь текстовый файл, вставляешь код, закрываешь. Меняешь название на scihub, а расширение на .py.
	
Создаёшь cmd.txt. Вставляешь:

```
cd "C:\Users\...\Sci-Hub"
python scihub.py DOI.txt
```

Создаёшь DOI.txt.

Складываешь все 3 файла в папку Sci-Hub.

Открываешь cmd.txt. "C:\Users\...\Sci-Hub" - путь к папке Sci-Hub. В неё загрузятся PDF-файлы.
<br><br>

Открываешь DOI.txt. Заполняешь ссылками на статьи.

Копируешь содержимое cmd.txt.

Win+R cmd Ctrl+V
<br><br>

Статьи можно склеить в один PDF-файл с помощью программы PDF-XChange Editor.

<https://rutracker.org/forum/viewtopic.php?t=5998062>