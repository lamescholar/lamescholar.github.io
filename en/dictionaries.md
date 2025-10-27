---
layout: page
comments: true
title: Dictionaries
---

GoldenDict - <https://github.com/goldendict/goldendict/releases>

```
<maxPictureWidth>
```

Dictionaries for GoldenDict:<br>
<https://rutracker.org/forum/viewtopic.php?t=3582459><br>
<https://rutracker.org/forum/viewtopic.php?t=3369767><br>
<http://dadako.narod.ru/paperpoe.htm><br>
<https://cloud.freemdict.com/index.php/s/pgKcDcbSDTCzXCs>

Creating dictionaries for GoldenDict:<br>
<http://languagehopper.blogspot.com/2013/06/how-to-make-your-own-stardictoldendict.html><br>
<https://code.google.com/archive/p/stardict-3/downloads>
<br><br>

#### Translators:

Yandex Translate - <https://translate.yandex.ru/>

Google Translate - <https://translate.google.com/>

[ChatGPT](/en/chatgpt)
<br><br>

#### Online dictionaries:

Multitran - <https://www.multitran.com/>

Collins COBUILD - <https://www.collinsdictionary.com/>

Oxford English Dictionary - <https://www-oed-com.i.ezproxy.nypl.org/>

Random House Unabridged Dictionary - <https://www.dictionary.com/>

Free Dictionary. Idioms and phrases - <https://idioms.thefreedictionary.com/>

Visual Dictionary - <http://www.visualdictionaryonline.com/>
<br><br>

#### Encyclopedias:

Encyclopaedia Britannica:<br>
<https://rutracker.org/forum/viewtopic.php?t=4891866><br>
<https://rutracker.org/forum/viewtopic.php?t=6307320><br>
<https://rutracker.org/forum/viewtopic.php?t=6304689><br>
<https://www.britannica.com/>

Encyclopedia Americana - <https://rutracker.org/forum/viewtopic.php?t=6311493>

Columbia Encyclopedia - <https://www.infoplease.com/encyclopedia>

Stanford Encyclopedia of Philosophy:<br>
<https://plato.stanford.edu/index.html><br>
<https://disk.yandex.ru/d/09mGI89C7r87vQ>

Encyclopedia of Philosophy - <https://www.myanonamouse.net/t/80064>

Larousse - <https://www.larousse.fr/encyclopedie>

Treccani - <https://www.treccani.it/>

Encyclopedia of Diderot and D'Alambert - <https://quod.lib.umich.edu/d/did/title/A.html>

Encyclopedia.com - <https://www.encyclopedia.com/>

World History - <https://www.worldhistory.org/>

Gallup - <https://news.gallup.com/topic/all-gallup-headlines.aspx>

Our World in Data - <https://ourworldindata.org/>

Statista - <https://www-statista-com.i.ezproxy.nypl.org/>
<br><br>

#### Fun command-line dictionary

Some StarDict dictionaries are hyphenated. They are not very convenient for GoldenDict, but they are great for Windows command-line.

To run StarDict dictionary in command-line

1) install sdcv:

MSYS - <https://www.msys2.org/>

`pacman - S mingw-w64-sdcv`

2) create system variable:<br>
STARDICT_DATA_DIR<Br>
C:\msys64\mingw64\bin\dict

3) put [stardict-dictd-web1913-2.4.2](https://github.com/ahacop/websters-dict-1913-stardict) into dict folder

4) add sdcv to PATH

Then:<br>
Win+R cmd<br>
sdcv

You can make .bat file:<br>
`C:\msys64\mingw64\bin\sdcv.exe`