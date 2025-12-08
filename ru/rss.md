---
layout: page
comments: true
title: RSS
---

RSS - это XML-файл, который фиксирует публикации на сайте. Открыв его RSS reader'ом, ты получаешь ленту последних публикаций. RSS-ленты обычно генерируют [блоги](/ru/blogs), [газеты](/ru/newspapers) и [журналы](/ru/articles).
<br><br>

yet another rss reader - <https://github.com/nkanaev/yarr>

Win+R

shell:startup

Вставь ярлык .exe файла. Теперь yarr будет запускаться при запуске системы.

Можно сделать закладку в браузере для адреса <http://127.0.0.1:7070/>

База данных программы находится в папке AppData\Roaming\yarr.
<br><br>

Чтобы компилировать последнюю версию, установи:

Go - <https://go.dev/dl/>

GCC - <https://jmeubank.github.io/tdm-gcc/>

Cygwin - <https://www.cygwin.com/install.html>

Во время установки Cygwin выбери, чтобы установился make.

Далее как описано здесь <https://github.com/nkanaev/yarr/blob/master/doc/build.md>

Запусти терминал Cygwin.

```
git clone https://github.com/nkanaev/yarr.git
cd yarr
make build_windows  # -> _output/windows/yarr.exe
```

Получишь yarr.exe в C:\cygwin64\home\имя пользователя\yarr\_output\windows

Или установи последний релиз: [yarr_windows_amd64_gui.zip](https://github.com/nkanaev/yarr/releases)
<br><br>

Ты можешь импортировать мои подписки:

<a href="/files/subscriptions.opml" download>subscriptions.opml</a>

Чтобы читать периодику на иностранных языках, используй Google Translate, встроенный в Google Chrome, для перевода на английский (Google Translate сносно переводит только на английский). Кликни правой кнопкой мыши по пустому месту, выбери Перевести на English. Либо используй ChatGPT:
<https://lamescholar.github.io/ru/chatgpt>
<br><br>

Как найти RSS-ленту? Добавь к URL:

/feed/

/rss

/rss.xml

Поищи RSS-ленту на странице.

Попробуй загуглить "URL rss".

Если нет результата, используй [Google Новости](https://news.google.com/home?hl=ru&gl=RU&ceid=RU:ru). Сделай такого рода запрос:

```
when:24h inurl:profile.ru
```

И добавь к URL "rss":

<https://news.google.com/search?q=when%3A24h%20inurl%3Aprofile.ru&hl=ru&gl=RU&ceid=RU%3Aru>

<https://news.google.com/rss/search?q=when%3A24h%20inurl%3Aprofile.ru&hl=ru&gl=RU&ceid=RU%3Aru>

В случае журнала с редкой публикацией можно расширить временной отрезок с 24h до 168h (1 неделя):

```
when:168h inurl:forbes.ru
```

<https://news.google.com/search?q=when%3A168h%20inurl%3Aforbes.ru&hl=ru&gl=RU&ceid=RU%3Aru>

<https://news.google.com/rss/search?q=when%3A168h%20inurl%3Aforbes.ru&hl=ru&gl=RU&ceid=RU%3Aru>

Также ты можешь сгенерировать RSS-ленту с помощью rss-bridge:

rss-bridge - <https://github.com/RSS-Bridge/rss-bridge>

XPathBridge - <https://rss-bridge.org/bridge01/#bridge-XPathBridge>

Чтобы использовать XPathBridge, тебе нужно найти XPath (путь к элементу в HTML-файле) необходимых элементов RSS-ленты. Нажми правой кнопкой мыши на элемент (заголовок, картинка, время) и выбери Посмотреть код. Нажми правой кнопкой мыши на строку кода и выбери Copy->Copy full XPath.

Пример использования XPathBridge для e-flux Notes:

```
https://www.e-flux.com/notes/

/html/body/div[1]/div[3]/div[1]/div[3]/div[2]/div

.//div[2]

Item description selector: .//div[3]

.//div[2]/a/@href

.//div[1]
```