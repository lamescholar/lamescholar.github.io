---
layout: page
comments: true
title: Аудиокниги
---

#### Источники:

AudioBook Bay - <https://audiobookbay.lu/member/advanced_search>

My Anonymouse - <https://www.myanonamouse.net/index.php>

<div style="border: 1px solid black; padding: 10px;">
<p>Интервью:</p>

<p><a href="https://www.myanonamouse.net/inviteapp.php">https://www.myanonamouse.net/inviteapp.php</a></p>

<p>IRC-клиент:</p>

<p>mIRC - <a href="https://rutracker.org/forum/viewtopic.php?t=2901572">https://rutracker.org/forum/viewtopic.php?t=2901572</a></p>

<p>AppData\Roaming\mIRC\scripts</p>

<p>HexChat - <a href="https://hexchat.github.io/downloads.html">https://hexchat.github.io/downloads.html</a></p>
</div>
<br>

#### Программы:

Winamp - <https://www.winamp.com/downloads/>

Отключить затихание:<br>
Preferences...->Plug-ins->Output->Nullsoft DirectSound Output->Fading<br>
on pause/stop - сними галочку<br>
on seek - сними галочку

<https://getwacup.com/community/index.php?topic=1081.0>
<br><br>

#### Аудиокнига с субтитрами

Допустим, ты нашёл аудиокнигу на немецком. Её можно перевести на английский (на русский перевод хуже).

У тебя mp3 и обложка аудиокниги.

1. С помощью [subsai](/ru/whisper) из mp3 делаешь субтитры (1.srt).

2. Переводишь субтитры (1.srt) с немецкого на английский с помощью Subtitle Edit + LM Studio + Qwen3-4B (2.srt).

3.  Subtitle Edit: Merge two SRT to one ASS/SSA... (1.ass)

4. Из mp3 и обложки делаешь видео с помощью ffmpeg.

	Установка ffmpeg:

	Chocolatey - <https://chocolatey.org/install>

	Открываешь командную строку с правами администратора. Правой кнопкой мыши по кнопке Пуск. Терминал (Администратор).

	choco install ffmpeg

	Команды:

	Win+R

	```
	cd путь к папке с mp3 и обложкой
	ffmpeg -loop 1 -i обложка.jpg -i "аудиокнига на немецком.mp3" -shortest out.mp4
	```

5. Вшиваешь субтитры (1.ass) в видео:

	Win+R

	```
	cd путь к папке с mp3 и обложкой
	ffmpeg -i 1.mp4 -vf ass=1.ass 2.mp4
	```

Получается что-то вроде фильма с субтитрами. Аудиокнига с субтитрами.

Субтитры можно не переводить. Например, хочешь послушать аудиокнигу на английском, но распознаёшь не все слова. Делаешь субтитры. Делаешь видео. Вшиваешь субтитры в видео. Получаешь аудиокнигу с субтитрами.