---
layout: post
tag: Reposts
comments: true
title: How to search and download unpopular and old files on the internet
---

Source: <https://medium.com/@ValdikSS/how-to-search-and-download-unpopular-and-old-files-on-the-internet-e5947ef507ba>
<br><br>

# How to search and download unpopular and old files on the internet

ValdikSS - Oct 14, 2017
<br><br>

Mostly media files. Totally legit, no kidding.

As sometimes happens, you want to download music album from 2007, of the artist known by 3.5 people, like a Spanish Ska-punk or a less-known European speedcore. Got torrent file, import it into client, quickly download up to 14.7% and… that’s it. The day, week passes by, but the percentage of downloaded data is not increased. You’re searching for that album in search engine, stumble upon forums with links only for registered users with “useful messages”, you register there, quickly flood 5 messages in deadly old topics, and finally get links for file sharing sites like rapidshare and megaupload, which are hundred years dead from now.
<br><br>

{:refdef: style="text-align: center;"}
![valdik1](/images/valdik1.webp)
{: refdef}

{:refdef: style="text-align: center;"}
<sub>Unfortunately very common situation when you try to download something old.</sub>
{: refdef}
<br>

That happens. Lately, unfortunately, it happens more and more often: copyright holders and law-enforcement authorities have taken up file sharing seriously; last year we seen closed or seized KickassTorrents, BlackCat Games, what.cd, btdigg, torrentzeu, EX.ua, fs.to, torrents.net.ua and all other websites. While you likely won’t face huge problems in finding fresh movie and TV/animated series rips even despite the repeatedly increased removal of content from search engines, torrent trackers and file sharing, searching for movie source (DVD or Blu-Ray) or just non-English and non-Russian 7-year-old TV rips could be challenging.
<br><br>

# Why would you ever need that?

- **Lack of DVD releases for some series**  
  The film could have been dubbed and aired on TV in some country, but never get on DVD. Cappers rip it and upload to file sharing sites or via Bittorrent, then DVD is released in another country without capped audio dub, for example, a French one. People are forced to download high quality DVDRip without French dub or relatively low quality TV rip with it.  
  As the times go by, less and less people download French TVRip, it got deleted from file sharing sites due to file inactivity. Downloading this release become rather nontrivial task.  
  One can solve the problem by muxing audio from TV rip to DVD video, but nobody did that and TV version died.
- **Different TV and DVD content**  
  For example, <a href="https://en.wikipedia.org/wiki/Daria" class="af nq" rel="noopener ugc nofollow" target="_blank">Daria</a> lost almost all music from TV version due to legal problems with re-licensing it for DVD. For a long time people were facing a choice between watching full version with all music and bad video quality or nice-looking DVD version, but without music.
- **Regional difference**  
  These are true for both video and music. W.I.T.C.H. series has aired with 4 different openings, only one of which got into DVD.
  Japanese versions of music albums are known for bonus tracks, which are missing in any other edition.

As you may already understand, everyone have own reason. Where do we download unpopular and old files?
<br><br>

# Usenet

Usenet is a distributed network of servers which synchronize data between them. Usenet structure resembles something in the middle between forums and email: so-called “newsgroups” (Usenet categories) have tree-style structure. Usenet users can join groups, read and write to it. Just as in email, Usenet messages have subject, which helps to organize discussion topic.  
Nowadays Usenet is primarily used for file sharing.
<br><br>

#### Usenet history

Emerged in 1979, network used direct modem connections to transfer information using UUCP and was generally an instrument for text communications. That time Usenet was a BBS competitor; there was special gateways between Usenet and Fidonet.  
As internet come, Usenet messaging switched to TCP/IP stack, using NNTP, which is still used even outside of Usenet (for example, you can read lots of public mail lists using <a href="http://www.gmane.org/" class="af nq" rel="noopener ugc nofollow" target="_blank">gmane</a> and RSS feeds via <a href="http://gwene.org/" class="af nq" rel="noopener ugc nofollow" target="_blank">gwene,</a> and unlike usual mail list, you can always go back into history, before you subscribed to that list.)
<br><br>

{:refdef: style="text-align: center;"}
![valdik2](/images/valdik2.webp)
{: refdef}
<br>

With more line speed, modern modems and its’ protocols, in early 90-s Usenet became a ground for file transfers: warez, music, videos. The algorithm is similar to one in Email: file is cut into several pieces (volumes), encoded using printable characters in 7-byte encoding using Base64 or uuencode, and sent to the newsgroup.  
7-bit encoding adds about 30% file transfer overhead. Usenet specification allowed using most ASCII symbols, not just printable ones, thus new file encoding algorithm yEnc emerged in 2001, adding only 1–2% of overhead. It quotes only newline symbols, NULL bytes and equal sign (=). yEnc is still the main algorithm of Usenet file transfers.

Integrity check and corrupted volume recovery is achieved with <a href="https://en.wikipedia.org/wiki/Parchive" class="af nq" rel="noopener ugc nofollow" target="_blank">Parchive</a>
<br><br>

{:refdef: style="text-align: center;"}
![valdik3](/images/valdik3.webp)
{: refdef}
<br>

Before 2008 big Usenet providers stored binary files for only 100–150 days (“retention time”). Since 2008 the biggest providers stopped deleting anything and store files forever, so one can download 8-year-old files without any problem, while mid-sized providers store files for 1000+ days which is not exactly bad also. Nowadays, text communication over Usenet is almost non-existent; the network is used primarily as file storage.

Circa mid 2001 the network has been spotted by copyright holders, forcing Usenet providers to delete copyrighted content, which largely influenced release consistency. Some providers created automatic systems to delete files under copyright, allowing copyright holders to delete information on their own. To stop or at least decelerate file deletion, enthusiasts begin to upload files with obfuscated file names or use password-protected archives, adding them into private, invite-only file index websites afterwards. These releases cannot be found or downloaded by usual means.

In modern Russia Usenet is known by only a few people, despite it was among two working links with the west in <a href="https://www.opendemocracy.net/od-russia/natalia-konradova/usenet-coup" class="af nq" rel="noopener ugc nofollow" target="_blank">1991 coup</a> (the second is Fido).  
Nowadays Usenet is most popular in countries with strict copyright laws with fines for downloading or uploading copyrighted content. Germany is an example of such country.  
Unlike Bittorrent, you cannot determine users’ IP address in Usenet, unless with cooperation with ISP or Usenet provider.
<br><br>

#### Connect to Usenet

Most likely, you won’t be able to join the network for free: you either would get low retention time (10–30 days) or low speed, or even access to text-only newsgroups. You need to buy access from any Usenet provider or reseller. Most providers offer two types of access: monthly subscription with unmetered data (unlimited) and data plan without time limit (block). If you’re interested in downloading files a few times a month, block access is good to go.  
Largest providers are: <a href="https://www.altopia.com/" class="af nq" rel="noopener ugc nofollow" target="_blank">Altopia</a>, <a href="http://www.giganews.com/" class="af nq" rel="noopener ugc nofollow" target="_blank">Giganews</a>, <a href="http://www.eweka.nl/en/home/" class="af nq" rel="noopener ugc nofollow" target="_blank">Eweka</a>, <a href="https://www.newshosting.com/" class="af nq" rel="noopener ugc nofollow" target="_blank">NewsHosting</a>, <a href="http://www.astraweb.com/" class="af nq" rel="noopener ugc nofollow" target="_blank">Astraweb</a>.

Now you somehow need to get nzb file with metainformation. This is something like a .torrent file for Usenet. Let’s use indexer search engine if you don’t have one.
<br><br>

#### Indexers

Public indexers are full of spam and viruses, their search capabilities are mediocre, but, nevertheless, they are good for old files uploaded 5 years ago or more.

Here are some of them:

- <a href="http://binsearch.info/" class="af nq" rel="noopener ugc nofollow" target="_blank">binsearch.info</a>
- <a href="http://binzb.com/" class="af nq" rel="noopener ugc nofollow" target="_blank">binzb.com</a>
- <a href="http://nzbindex.com/" class="af nq" rel="noopener ugc nofollow" target="_blank">nzbindex.com</a>
- <a href="http://nzbsearch.net/" class="af nq" rel="noopener ugc nofollow" target="_blank">nzbsearch.net</a>
- <a href="http://www.nzbking.com/" class="af nq" rel="noopener ugc nofollow" target="_blank">nzbking.com</a>

Free indexers with registration requirement are more suitable for fresh files. Their catalog structure is good, the releases have not only the name but the description and picture.

- <a href="https://nzbfinder.ws/" class="af nq" rel="noopener ugc nofollow" target="_blank">nzbfinder.ws</a>
- <a href="http://nzbid.org/" class="af nq" rel="noopener ugc nofollow" target="_blank">nzbid.org</a>
- <a href="https://nzbnoob.com/" class="af nq" rel="noopener ugc nofollow" target="_blank">nzbnoob.com</a>
- <a href="https://nzb.ag/" class="af nq" rel="noopener ugc nofollow" target="_blank">nzb.ag</a>
- <a href="http://nzbfriends.com/" class="af nq" rel="noopener ugc nofollow" target="_blank">nzbfriends.com</a>
- <a href="https://www.usenet-crawler.com/" class="af nq" rel="noopener ugc nofollow" target="_blank">usenet-crawler.com</a>
- <a href="https://drunkenslug.com/" class="af nq" rel="noopener ugc nofollow" target="_blank">drunkenslug.com</a>
- <a href="https://nzbgeek.info/" class="af nq" rel="noopener ugc nofollow" target="_blank">nzbgeek.info</a>

I especially recommend the last two, they are capable of searching obfuscated releases.  
There are indexes focused only one subject, for example, <a href="https://anizb.org/" class="af nq" rel="noopener ugc nofollow" target="_blank">anizb</a> for anime and <a href="https://www.albumsindex.com/" class="af nq" rel="noopener ugc nofollow" target="_blank">albumsindex</a> for music.
<br><br>

#### Downloading from Usenet

Let’s try to download <a href="http://www.imdb.com/title/tt1296373/" class="af nq" rel="noopener ugc nofollow" target="_blank"><strong>The FP</strong></a>, an unpopular and mostly unknown movie from 2011, the 1080p BDRip of which cannot be found in the usual internet.  
You need to find nzb file and import it into downloading program like <a href="http://nzbget.net/" class="af nq" rel="noopener ugc nofollow" target="_blank">NZBGet</a> or <a href="https://sabnzbd.org/" class="af nq" rel="noopener ugc nofollow" target="_blank">SABnzbd</a>.

Go to <a href="http://www.nzbking.com/" class="af nq" rel="noopener ugc nofollow" target="_blank">nzbking.com</a>, search for “the.fp.2011”.
<br><br>

{:refdef: style="text-align: center;"}
![valdik4](/images/valdik4.webp)
{: refdef}
<br>

This file has only 1 part of 3867. You cannot download such file, the indexer shows this in red.
<br><br>

{:refdef: style="text-align: center;"}
![valdik5](/images/valdik5.webp)
{: refdef}
<br>

Password protected files are usually fakes.
<br><br>

{:refdef: style="text-align: center;"}
![valdik6](/images/valdik6.webp)
{: refdef}
<br>

Second page shows us a sign of proper DVDRip — the filesize is good, no password.
<br><br>

{:refdef: style="text-align: center;"}
![valdik7](/images/valdik7.webp)
{: refdef}
<br>

Third page shows us BDRip and several DVDRips, which looks good (based on file size and upload date).

Choose files you want to download, press “Download NZB”, import .nzb into NZBGet or SABnzbd with configured Usenet account data.  
The file is being downloaded with full ISP link speed.
<br><br>

{:refdef: style="text-align: center;"}
![valdik8](/images/valdik8.webp)
{: refdef}
<br>

As file finished downloading, NZBGet would automatically unpack archives and delete them, keeping only unpacked data. You’ve got 6.74 of data, which was uploaded 4.5 years ago, in only 15 minutes, hooray!
<br><br>

# IRC / DCC / XDCC

Internet Relay Chat is an old protocol for text communications which is still popular among open-source software developers, torrent trackers administrators, anime lovers and authors of botnet CnCs, because of its simplicity. Emerged in 1989, IRC quickly became the standard for text chats on the internet for a long years, and conceded its popularity to ICQ and Jabber only in mid 2000s. IRC support file transfer using DCC, which was first used for automatic file sharing by Xabi, in Xabi DCC (hence the name — XDCC).

Now you have IRC channels and even whole servers only for file transfers using XDCC. Almost any anime release group, sometimes even without a website, have it’s own bot, which serves all group’ files. XDCC popularity is driven by ease of using and administrating file sharing bots: uploader need only to upload the file itself using FTP for example, and bot will automatically add that new file to index and notify channel users of it (if it’s a new episode of a TV series as an example).

Special private IRC networks are used for warez, fresh and not so movies, music, games, boots. XDCC is hardly known by copyright agencies, that’s why you can find lots of stuff you cannot find in other places.
<br><br>

#### Indexers

Most (but not all) XDCC bots are indexed with special scripts, providing web interface for search engine.

Indexers of generic content:

- <a href="http://ixirc.com/" class="af nq" rel="noopener ugc nofollow" target="_blank">ixirc.com</a>
- <a href="http://www.xdcc.eu/" class="af nq" rel="noopener ugc nofollow" target="_blank">xdcc.eu</a>
- <a href="http://sunxdcc.com/" class="af nq" rel="noopener ugc nofollow" target="_blank">sunxdcc.com</a>
- <a href="https://www.cr4wl.ga/" class="af nq" rel="noopener ugc nofollow" target="_blank">cr4wl.ga</a>

Anime indexers:

- <a href="https://news.kae.re/" class="af nq" rel="noopener ugc nofollow" target="_blank">news.kae.re</a>
- <a href="http://nibl.co.uk/bots.php" class="af nq" rel="noopener ugc nofollow" target="_blank">nibl.co.uk</a>
- <a href="http://intel.haruhichan.com/" class="af nq" rel="noopener ugc nofollow" target="_blank">intel.haruhichan.com</a>
<br><br>

#### How to download from IRC

You’ll need IRC client. Almost any client will work, overwhelming majority of clients support DCC. Join the server depending on the content you’re interested in, and download.  
The biggest servers with **books**:

- irc.undernet.org, \#bookz room
- irc.irchighway.net, \#ebooks room

**Warez**:

- irc.criten.net, \#elitewarez room
- irc.infatech.net, \#elitewarez room
- irc.scenep2p.net, \#the.source room

**Movies**:

- irc.abjects.net, \#moviegods room
- irc.abjects.net, \#beast-xdcc room

**Western and Japanese animation**:

- irc.rizon.net, \#news room
- irc.xertion.org, \#cartoon-world room

All bots accept `!find` or `@find`commands for searching files, sending you search results with a direct message. Searching for a popular query will get you literally spammed with search results, that’s why it’s sane to use `@search` command where available. This command will trigger special indexer bot to send you search results in one file over DCC.

Let’s try to download “How Music Got Free” — a great book about music industry, music sharing technologies and a person who stole almost 2000 different albums and uploaded it to the internet.
<br><br>

{:refdef: style="text-align: center;"}
![valdik9](/images/valdik9.webp)
{: refdef}
<br>

The bot reacts to `@search` request and sends results in a zipped text file over DCC.
<br><br>

{:refdef: style="text-align: center;"}
![valdik10](/images/valdik10.webp)
{: refdef}
<br>

Let’s send download request query to the bot.
<br><br>

{:refdef: style="text-align: center;"}
![valdik11](/images/valdik11.webp)
{: refdef}
<br>

And accept it!
<br><br>

{:refdef: style="text-align: center;"}
![valdik12](/images/valdik12.webp)
{: refdef}
<br>

If you found a file using file indexer, you don’t need to search for it on the channel. Just send download query to the bot right away using the command from indexer site.
<br><br>

# DC++

Direct Connect network is based on client-server architecture, where all the non-filesharing communications are done via server, which is called hub. DC++ supports sharing the whole directories, can search for exact file types (audio, video, archives, documents, disk images), and has search engine which is not bound to file name. DC++ is most known for build-in chat, which was very handy in local networks of early days.  
Such hubs were popular in Russia, some of them were maintained by ISPs themselves. Siberian “GoodLine” ISP advertized own DC++ hub on advertising hoardings and even had a special software inside set-top boxes to deliver users new movies right to the TV.  
That was the biggest hub of the world, with more than 100000 users.
<br><br>

{:refdef: style="text-align: center;"}
![valdik13](/images/valdik13.webp)
{: refdef}
<br>

Due to ease of file sharing (you need only to put a tick against directory to be shared), you can find weird, exotic junk, which is, as the user thinks, nobody even remember, but he still share it with others, just in case.
<br><br>

{:refdef: style="text-align: center;"}
![valdik14](/images/valdik14.webp)
{: refdef}

{:refdef: style="text-align: center;"}
<sub>11-year-old videotutorial is seeded by 3 persons. Nobody would ever want to watch it, believe me.</sub>
{: refdef}
<br>

#### How to download from DC++

You’ll need any DC++ client. <a href="http://www.flylinkdc.com/" class="af nq" rel="noopener ugc nofollow" target="_blank">FlylinkDC++</a> is a good to go for Windows (it supports Bittorrent, too). Linux users choose <a href="https://sourceforge.net/projects/eiskaltdcpp/" class="af nq" rel="noopener ugc nofollow" target="_blank">EiskaltDC++</a> or <a href="https://airdcpp-web.github.io/" class="af nq" rel="noopener ugc nofollow" target="_blank">AirDC++ Web</a>.

Join some DC++ hubs, the more the better. DC++ hublist is available in the clients itself, but you can also access it using <a href="http://www.thehublist.com/?do=hubs" class="af nq" rel="noopener ugc nofollow" target="_blank">this special web page</a> and copy address from there.

I highly recommend you to configure “Active Mode” and set up port forwarding, otherwise you won’t be able to download files from users in “Passive Mode” and your search results would be limited.
<br><br>

{:refdef: style="text-align: center;"}
![valdik15](/images/valdik15.webp)
{: refdef}
<br>

Searching and downloading is self-explanatory: type search query, choose content type if you want, press “search”, double-click search result to download. You can also see a list of all shared files of exact user (and download all files from selected folder) by right-clicking search result and selecting corresponding menu item.
<br><br>

{:refdef: style="text-align: center;"}
![valdik16](/images/valdik16.webp)
{: refdef}
<br>

If the file you were searching for is not found, it’s worth to repeat your search query from time to time. People tend to start DC client only when they need to download something, so you need to catch the wave to find files from such users.

Simultaneous search for multiple files may be hard due to NMDC protocol limitations. Search results may intermix and show up for different search queries, that’s why it’s safer to perform only one search at a time. ADC hubs don’t have such limitation, but they are dismally non-existent (their URI starts with `adc://`, not `dchub://`).
<br><br>

#### Indexers

Built-in search finds files only in online users’ lists, that’s why indexers are very convenient for searching rare files.

As far as I know, the only DC++ indexer is <a href="http://spacelib.dlinkddns.com/" class="af nq" rel="noopener ugc nofollow" target="_blank">spacelib.dlinkddns.com</a> (and it’s other address is <a href="http://dcpoisk.no-ip.org/" class="af nq" rel="noopener ugc nofollow" target="_blank">dcpoisk.no-ip.org</a>). Search is build upon Sphinx engine with morphology support. Search results consists of magnet links you can add to download queue in DC++ client.  
Sometimes it’s down for long times. For example, last time it was down for 2 months straight.
<br><br>

# eDonkey2000 (ed2k), Kad

ed2k is a protocol of decentralized file transfer with centralized hub for search queries and establishing connection between users, just like DC++. Itr used to be \#1 protocol for file sharing for all social groups before seizure of the most popular server, Razorback 2, back in 2006, and increasing popularity of BitTorrent.

eDonkey 2000 is still alive. Merely because of decentralized Kad protocol, which was implemented right before Razorback 2 and original client server went out of service.

You can find almost the same content as in DC++: old TV series with different dub, various music, games, warez, old programming books, math and biology books. Of course, new released are here too. The protocol supports chat functionality, but you’re unlikely would be able to use it as it’s disabled by default in all clients, your messages just won’t be shown.
<br><br>

#### How to download from eDonkey2000/KAD

As you may guess, you’ll need ed2k client. <a href="http://www.amule.org/" class="af nq" rel="noopener ugc nofollow" target="_blank">aMule</a> is a good choise for Linux. Windows users should probably use <a href="http://www.emule-project.net/" class="af nq" rel="noopener ugc nofollow" target="_blank">eMule</a>, although it’s not being updated since 2011.  
It’s highly recommended to set up port forwarding to be able to download from users behind NAT (LowID).

Searching and downloading process is very similar to one in DC++. Type search query, get results from online users, double-click on the file to begin download.  
Query result would be shown even if none of the users have it in full, but only parts of it.

Let’s find “<a href="http://www.imdb.com/title/tt0498329/" class="af nq" rel="noopener ugc nofollow" target="_blank"><strong>We Live In Public</strong></a>”, a less-known documentary from 2009 about the internet of 90s. A part of this movie tells about pseudo.com video streaming service from 1993, which is partially foretold modern internet.

Just type search query, press the button and wait for results:
<br><br>

{:refdef: style="text-align: center;"}
![valdik17](/images/valdik17.webp)
{: refdef}
<br>

Double-click to begin download.
<br><br>

{:refdef: style="text-align: center;"}
![valdik18](/images/valdik18.webp)
{: refdef}
<br>

Downloading one file can take weeks or even months. For some unknown reason, most ed2k users have disgusting internet speed and show up in the network for only some hours per week, or even less. Be patient.
<br><br>

# Soulseek

Soulseek is a centralized network for p2p music sharing, created in 2000 by one of Napster developers. It’s known in IDM community, and is still in active development. Group and private chats, friend-to-friend only file sharing, tag and bitrate-aware search are among the other things of this network.  
Some search queries are censored.

The official proprietary <a href="http://www.soulseekqt.net/news/" class="af nq" rel="noopener ugc nofollow" target="_blank">SoulseekQt</a> is the most popular one, with two unofficial clients also available: <a href="https://www.nicotine-plus.org/" class="af nq" rel="noopener ugc nofollow" target="_blank">Nicotine+</a> and <a href="http://museek-plus.org/" class="af nq" rel="noopener ugc nofollow" target="_blank">Museek+</a>.
<br><br>

# BitTorrent DHT

All modern BitTorrent clients are able to find peers using distributed hash table (DHT). This feature is used not only by copyright-oriented companies to monitor users and send them copyright infringement messages, but also by DHT indexers, to receive torrent file with infohash from third-party DHT query and save it to the database. Such indexers could be handy to find rare or unpublished torrents by file or directory name, or to search similar torrents with potentially more seeds.

The most known but nowadays dead indexer is <a href="https://habrahabr.ru/post/124496/" class="af nq" rel="noopener ugc nofollow" target="_blank">btdigg</a>, the other sites came to replace it:

- <a href="https://bitsnoop.com/" class="af nq" rel="noopener ugc nofollow" target="_blank">bitsnoop.com</a>
- <a href="https://www.godht.com/" class="af nq" rel="noopener ugc nofollow" target="_blank">godht.com</a>
- <a href="https://btdb.in/" class="af nq" rel="noopener ugc nofollow" target="_blank">btdb.in</a>
- <a href="https://www.digbt.org/" class="af nq" rel="noopener ugc nofollow" target="_blank">digbt.org</a>
- <a href="https://btdb.in/" class="af nq" rel="noopener ugc nofollow" target="_blank">btdb.in</a>
- <a href="http://btkitty.bid/" class="af nq" rel="noopener ugc nofollow" target="_blank">btkitty.bid</a>
- <a href="http://kikibt.net/" class="af nq" rel="noopener ugc nofollow" target="_blank">kikibt.net</a>
- <a href="https://btdig.com/" class="af nq" rel="noopener ugc nofollow" target="_blank">btdig.com</a> (not related to original btdigg, although wikipedia page assures the contrary)

DHT indexers are known to live short lives: two of my favourites, fastbot and BTKitty.red, are inaccessible when I write this article.
<br><br>

# File sharing sites and FTP servers

Almost every region has it’s own local file sharing site, which is popular among exact lingual group. For example, you can find lots of Czech and Slovak content on <a href="https://uloz.to/" class="af nq" rel="noopener ugc nofollow" target="_blank">uloz.to;</a> <a href="http://www.zone-telechargement.ws/" class="af nq" rel="noopener ugc nofollow" target="_blank">zone-telechargement.ws</a> is good for French content, while <a href="http://chomikuj.pl/" class="af nq" rel="noopener ugc nofollow" target="_blank">chomikuj.pl</a> is for Polish media.

FTP indexers don’t find requested file so often, but give it a try nevertheless:

- <a href="http://www.mmnt.net/" class="af nq" rel="noopener ugc nofollow" target="_blank">mmnt.net</a>
- <a href="http://www.searchftps.net/" class="af nq" rel="noopener ugc nofollow" target="_blank">searchftps.net</a>
- <a href="http://filemare.com/en" class="af nq" rel="noopener ugc nofollow" target="_blank">filemare.com</a>
- <a href="http://ftpsearch.lostclus.kiev.ua/" class="af nq" rel="noopener ugc nofollow" target="_blank">ftpsearch.lostclus.kiev.ua</a>
- <a href="http://www.filewatcher.com/" class="af nq" rel="noopener ugc nofollow" target="_blank">filewatcher.com</a>
- <a href="http://krasfs.ru/" class="af nq" rel="noopener ugc nofollow" target="_blank">krasfs.ru</a>
- <a href="http://ftplike.com/" class="af nq" rel="noopener ugc nofollow" target="_blank">ftplike.com</a>

File sharing websites search engines are also not so effective, but don’t forget about them:

- <a href="http://www.filediva.com" class="af nq" rel="noopener ugc nofollow" target="_blank">filediva.com</a>
- <a href="http://rapid-search-engine.com" class="af nq" rel="noopener ugc nofollow" target="_blank">rapid-search-engine.com</a>
- <a href="http://www.alluc.ee/" class="af nq" rel="noopener ugc nofollow" target="_blank">alluc.ee</a>

You could find lots of content on ex.ua until very recently, but unfortunately it’s closed now, what a pity.
<br><br>

# How to search scene releases

It’s not always sufficient to just search for content name, you could let **scene releases** slip though your fingers.

> The **Warez scene**, often referred to as **The Scene**, is an underground community of people that specialize in the distribution of copyrighted material, including television shows and series, movies, music, music videos, games (all platforms), applications (all platforms), ebooks, and pornography. The Scene is meant to be hidden from the public, only being shared with those within the community. However, as files were commonly leaked outside the community and their popularity grew, some individuals from The Scene began leaking files and uploading them to filehosts, torrents and ed2k.
>
> <a href="https://en.wikipedia.org/wiki/Warez_scene" class="af nq" rel="noopener ugc nofollow" target="_blank">https://en.wikipedia.org/wiki/Warez_scene</a>

Scene releases are known for short or intentionally garbled names to prevent it from searching with usual means by file name. To determine proper name, you have to search for the scene release in a special scene release indexers: <a href="https://layer13.net/" class="af nq" rel="noopener ugc nofollow" target="_blank">layer13.net</a>, <a href="http://pre.corrupt-net.org/" class="af nq" rel="noopener ugc nofollow" target="_blank">pre.corrupt-net.org</a> and <a href="http://predb.me/" class="af nq" rel="noopener ugc nofollow" target="_blank">predb.me</a>.

Let’s determine scene release name of We Live In Public from PUZZLE, using Layer13:
<br><br>

{:refdef: style="text-align: center;"}
![valdik19](/images/valdik19.webp)
{: refdef}
<br>

NFO name is “puzzle-wlip.nfo”. Archive names are in 99% cases are the same as NFO name, so let’s try to search for “puzzle-wlip” on a Usenet indexer:
<br><br>

{:refdef: style="text-align: center;"}
![valdik20](/images/valdik20.webp)
{: refdef}
<br>

How we can download a DVD image, hooray!

Usual search engines like Google are not always your helpful friend. First, Google follows DMCA and deletes (hides) copyright-restricted content. Second, it could be rather nontrivial to find content with special symbols: try search for *W.I.T.C.H.*, and you’ll get *Witch*, *The Witch* and *Blair Witch* results.  
I prefer <a href="https://duckduckgo.com/" class="af nq" rel="noopener ugc nofollow" target="_blank">DuckDuckGo</a>, <a href="https://www.bing.com/" class="af nq" rel="noopener ugc nofollow" target="_blank">Bing</a> and meta search engine <a href="https://searx.laquadrature.net/" class="af nq" rel="noopener ugc nofollow" target="_blank">SearX</a> — sometimes you find materials unavailable anywhere else.  
If you’re interested in a release of exact language, it’s sane to search by localized name which you can get from Wikipedia, IMDb or other similar websites.

Anime loves are free to use <a href="http://anidb.net" class="af nq" rel="noopener ugc nofollow" target="_blank">anidb,</a> which stores all the information about all releases. Group information is usually contains the website link or IRC channel where you can talk to its members and download files using XDCC.
<br><br>

{:refdef: style="text-align: center;"}
![valdik21](/images/valdik21.webp)
{: refdef}
<br>

Beside the source, video resolution, audio and subtitle language, anidb stores TTH hash for DC++ and ed2k link for eDonkey2000 of each known file.
<br><br>

{:refdef: style="text-align: center;"}
![valdik22](/images/valdik22.webp)
{: refdef}
<br>

# The end

That’s how I search for files on the internet. This article does not contain obvious things like ordering disks from Amazon or Ebay or searching on popular Torrent trackers. All described methods are good for European and USA media content, but I didn’t have the opportunity to search for Arab or Indian content, so I can’t say would it be effective or not in that case.
