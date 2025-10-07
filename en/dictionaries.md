---
layout: page
comments: true
title: Dictionaries
---

#### Programs:

GoldenDict - <https://sourceforge.net/projects/goldendict/files/early%20access%20builds/>

```
<maxPictureWidth>
```

Dictionaries for GoldenDict:<br>
<https://rutracker.org/forum/viewtopic.php?t=3582459><br>
<https://rutracker.org/forum/viewtopic.php?t=3369767><br>
<http://dadako.narod.ru/paperpoe.htm><br>
<https://cloud.freemdict.com/index.php/s/pgKcDcbSDTCzXCs><br>
<https://github.com/lxs602/1911-and-1922-Encyclopaedia-Britannica>

Creating dictionaries for GoldenDict:<br>
<http://languagehopper.blogspot.com/2013/06/how-to-make-your-own-stardictoldendict.html><br>
<https://code.google.com/archive/p/stardict-3/downloads>
<br><br>

#### Translators:

Yandex Translate - <https://translate.yandex.ru/>

Google Translate - <https://translate.google.com/>

[ChatGPT](/en/chatgpt)
<br><br>

#### Dictionaries:

Multitran - <https://www.multitran.com/>

Collins COBUILD - <https://www.collinsdictionary.com/>

Oxford English Dictionary - <https://www-oed-com.i.ezproxy.nypl.org/>

Random House Unabridged Dictionary - <https://www.dictionary.com/>

Free Dictionary. Idioms and phrases - <https://idioms.thefreedictionary.com/>

Visual Dictionary - <http://www.visualdictionaryonline.com/>
<br><br>

#### Encyclopedias:

Encyclopaedia Britannica:<br>
<https://rutracker.org/forum/viewtopic.php?t=6307320><br>
<https://rutracker.org/forum/viewtopic.php?t=6304689><br>
<https://www.britannica.com/>

Encyclopedia Americana - <https://rutracker.org/forum/viewtopic.php?t=6311493>

Columbia Encyclopedia - <https://www.infoplease.com/encyclopedia>

Stanford Encyclopedia of Philosophy - <https://plato.stanford.edu/index.html>

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

Some StarDict dictionaries come hyphenated. They are not very convenient for GoldenDict, but they are great for Windows command-line.

To run StarDict dictionary in command-line, install sdcv:

MSYS - <https://www.msys2.org/>

`pacman - S mingw-w64-sdcv`

Create system variable:<br>
STARDICT_DATA_DIR<Br>
C:\msys64\mingw64\bin\dict

Put [stardict-dictd-web1913-2.4.2](https://github.com/ahacop/websters-dict-1913-stardict) into dict folder.

Add sdcv to PATH. Then:<br>
Win+R cmd<br>
sdcv

You can make .bat file:<br>
`C:\msys64\mingw64\bin\sdcv.exe`