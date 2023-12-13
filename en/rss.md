---
title: RSS
---

RSS is XML file that collects updates on some site, so with RSS reader you get a feed of recent updates. Usually [blogs](/en/blogs), [newspapers](/en/newspapers), and [magazines](/en/articles) generate RSS feed.
<br><br>

yet another rss reader - <https://github.com/nkanaev/yarr>

Win+R

shell:startup

Paste shortcut of .exe file. Now yarr will start at system startup.

You can make a bookmark in browser for address <http://127.0.0.1:7070/>

To compile actual version install:

Go - <https://go.dev/dl/>

GCC - <https://jmeubank.github.io/tdm-gcc/>

Cygwin - <https://www.cygwin.com/install.html>

While installing Cygwin select to install make.

Then as described here <https://github.com/nkanaev/yarr/blob/master/doc/build.md>

Start Cygwin terminal.

```
git clone https://github.com/nkanaev/yarr.git
cd yarr
make build_windows  # -> _output/windows/yarr.exe
```

You'll get yarr.exe in C:\cygwin64\home\your username\yarr\_output\windows

[yarr.exe compiled by me](/files/yarr.exe)

You can import my subscriptions:

<a href="/files/subscriptions.opml" download>subscriptions.opml</a>

To read foreign languages use Google Chrome in-build Google Translate. Right-click some blank space, choose Translate to English.
<br><br>

How to find RSS feed? Add to URL:

/feed/

/rss

/rss.xml

Look for RSS feed on the page.

Try to google ""URL rss".

If no result, use [Google News](https://news.google.com/home?hl=en-US&gl=US&ceid=US:en). Make this kind of search:

when:24h inurl:washingtonpost.com

And add rss to URL:

<https://news.google.com/search?q=when%3A24h%20inurl%3Awashingtonpost.com&hl=en-US&gl=US&ceid=US%3Aen>

<https://news.google.com/rss/search?q=when%3A24h%20inurl%3Awashingtonpost.com&hl=en-US&gl=US&ceid=US%3Aen>

In case of magazine with rare publication you can extend period of time from 24h to 168h (1 week):

when:168h inurl:spectator.co.uk

<https://news.google.com/search?q=when%3A168h%20inurl%3Aspectator.co.uk&hl=en-GB&gl=GB&ceid=GB%3Aen>

<https://news.google.com/rss/search?q=when%3A168h%20inurl%3Aspectator.co.uk&hl=en-GB&gl=GB&ceid=GB%3Aen>

Also you can generate RSS feed using rss-bridge:

rss-bridge - <https://github.com/RSS-Bridge/rss-bridge>

XPathBridge - <https://rss-bridge.org/bridge01/#bridge-XPathBridge>

To use XPathBridge, you need to find XPath (path to element in HTML file) of necessary elements of RSS feed. Right click on the element (title, image, time) and select Inspect. Right click the code line and select Copy->Copy full XPath.

Example of XPathBridge use for e-flux Notes:

```
https://www.e-flux.com/notes/

/html/body/div[1]/div[3]/div[1]/div[3]/div[2]/div

.//div[2]

Item description selector: .//div[3]

.//div[2]/a/@href

.//div[1]
```