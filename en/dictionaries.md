---
layout: page
comments: true
title: Dictionaries
---

English is my second language. Quite often, I need to look up words which is really convenient with GoldenDict. I use it not only for dictionaries. I also found several encyclopedias. It is a really convenient way to quickly look up stuff, offline. Your own little reference library.
<br><br>

GoldenDict-ng - <https://github.com/xiaoyifang/goldendict-ng/releases>

article-style.css:

```
body, p, tr, li {
	font-family: Arial !important;
	font-size: 14.5px !important;
	line-height: 1.3 !important;
}

img {
	max-width: 500px !important;
	height: auto;
}
```

Dictionaries for GoldenDict:<br>
<https://rutracker.org/forum/viewtopic.php?t=3582459><br>
<http://dadako.narod.ru/paperpoe.htm><br>
<https://cloud.freemdict.com/index.php/s/pgKcDcbSDTCzXCs>

Creating dictionaries for GoldenDict:<br>
<http://languagehopper.blogspot.com/2013/06/how-to-make-your-own-stardictoldendict.html><br>
<https://code.google.com/archive/p/stardict-3/downloads>
<br><br>

Google Translate - <https://translate.google.com/>
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

Oxford Reference - <https://www-oxfordreference-com.i.ezproxy.nypl.org/>

Encyclopedia.com - <https://www.encyclopedia.com/>

Encyclopaedia Britannica:<br>
<https://rutracker.org/forum/viewtopic.php?t=4891866><br>
<https://rutracker.org/forum/viewtopic.php?t=6307320><br>
<https://rutracker.org/forum/viewtopic.php?t=6304689><br>
<https://www.britannica.com/><br>
<https://academic.eb.com/levels/collegiate><br>
<https://en.wikisource.org/wiki/1911_Encyclop%C3%A6dia_Britannica>

Encyclopedia Americana - <https://rutracker.org/forum/viewtopic.php?t=6311493>

Columbia Encyclopedia - <https://www.infoplease.com/encyclopedia>

Stanford Encyclopedia of Philosophy - <https://plato.stanford.edu/index.html>

Internet Encyclopedia of Philosophy - <https://iep.utm.edu/metaethi/>

Encyclopedia of Philosophy - <https://www.myanonamouse.net/t/80064>

Encyclopedia of Diderot and D'Alambert - <https://quod.lib.umich.edu/d/did/title/A.html>

Encyclopedia.com - <https://www.encyclopedia.com/>

World History - <https://www.worldhistory.org/>

Larousse - <https://www.larousse.fr/encyclopedie>

Treccani - <https://www.treccani.it/>

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