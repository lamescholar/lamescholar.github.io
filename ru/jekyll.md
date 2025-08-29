---
comments: true
title: Jekyll
---

С помощью [Jekyll](https://jekyllrb.com/) (генератор статических сайтов) и [GitHub Pages](https://pages.github.com/) (хостинг, на котором работает Jekyll) можно создать бесплатный статический сайт для своего блога. Лимит размера - 1 ГБ.
<br><br>

Для создания сайта необходимо зарегистрироваться на GitHub:

<https://github.com/>
<br><br>

Для создания сайта необходимо установить:

Git - <https://git-scm.com/download/win>

Jekyll - <https://jekyllrb.com/docs/installation/windows/>
<br><br>

#### Создание сайта

Вместо username использую твой username на GitHub.

Отправляйся в командную строку:

Win+R cmd

```
git init username.github.io
cd username.github.io
git checkout --orphan main
jekyll new --skip-bundle .
bundle install
git add .
git commit -m "first commit"
git remote add origin https://github.com/username/username.github.io.git
git push -u origin main
```

Твой сайт будет расположен по адресу https://username.github.io/

Источник: <https://docs.github.com/ru/pages/setting-up-a-github-pages-site-with-jekyll/creating-a-github-pages-site-with-jekyll>
<br><br>

#### Информация на сайте

В файле _config.yml заполняешь title, author, email, url, description (его можно удалить). В файле about.markdown прописываешь описание сайта.
<br><br>

#### Создание страницы

Создай .md файл в папке сайта. Например, page.md. Тогда на твоём сайте появится страничка по адресу https://username.github.io/page. Можешь поместить файл в папку folder.  Тогда на твоём сайте появится страничка по адресу https://username.github.io/folder/page.
<br><br>

#### Создание поста

<https://jekyllrb.com/docs/posts/>
<br><br>

#### Форматирование

```
1) Жирный текст - **жирный текст**
2) Курсив - *курсив*
3) Заглавие (в начале текста):
---
comments: true
title: Заглавие
---
4) Заголовок - # текст заголовка
5) Подзаголовок - #### текст подзаголовка
6) Новый абзац - пустая строка
7) Выделение ссылки - <ссылка>
8) Ссылка - [текст](ссылка)
9) Ссылка на страницу сайта: [текст](/папка/страница)
10) Ссылка туда и обратно:
текст<a href="#note" id="note-back">†</a>

<a href="#note-back" id="note">†</a> текст примечания
11) Ссылка на место в тексте:
[Place](#place)

<a id="place"></a>
12) Содержание:
#### Содержание
[Введение](#introduction)

<a id="introduction"></a>
#### Введение
13) Разрыв строки - <br>
14) Пустая строка (двойной разрыв строки) - <br><br>
15) Примечание:
текст[^1] текст[^2]

[^1]: текст примечания

	текст примечания

[^2]: текст примечания
16) Цитата:
> цитата
>
> продолжение цитаты
17) Маленький текст - <sub>текст</sub>
```

Блок кода - <https://docs.github.com/ru/get-started/writing-on-github/working-with-advanced-formatting/creating-and-highlighting-code-blocks>

<https://www.markdownguide.org/basic-syntax/>
<br><br>

#### Добавление картинки

Допустим, ты положил картинку image.png в папку images.

Как разместить картинку на странице:

```
![Описание картинки](/images/image.png)
```

В центре:

```
{:refdef: style="text-align: center;"}
![Описание картинки](/images/image.png)
{: refdef}
```

Со ссылкой:

```
{:refdef: style="text-align: center;"}
[![Описание картинки](/images/image.png)](ссылка)
{: refdef}
```
<br>

#### Добавление аудио

<https://stackoverflow.com/questions/63701944/how-to-embed-audio-into-a-jekyll-blog>
<br><br>

#### Добавление видео

<https://github.com/nathancy/jekyll-embed-video>

<https://stackoverflow.com/questions/48876911/embedded-local-mp4-not-playing-in-chrome-when-running-jekyll-serve-econnreset>
<br><br>

#### Добавление иконки сайта

<https://medium.com/@xiang_zhou/how-to-add-a-favicon-to-your-jekyll-site-2ac2179cc2ed>
<br><br>

#### Обновление сайта

Win+R cmd

```
cd username.github.io
git add .
git commit -m "new commit"
git push
```

Можно создать .bat файл и поместить в него эти команды. Тогда коммит можно сделать двумя кликами. Чтобы командная строка не закрывалась сразу после выполнения команд, добавь команду pause.
<br><br>

#### Запуск сайта локально

Во избежание ошибки, необходимо добавить webrick в Gemfile:

```
cd username.github.io
bundle add webrick
```

Запуск сайта:

```
cd username.github.io
bundle exec jekyll serve
```

Проходишь по выданному адресу.
<br><br>

#### Фильтрация зоны навигации (правый верхний угол)

Прописываешь в _config.yml:

```
header_pages:
  -about.markdown
```
<br>

#### Изменение размера заглавия

Заходишь в папку minima. На Windows она находится где-то здесь:

C:\Ruby32-x64\lib\ruby\gems\3.2.0\gems\minima-2.5.1

Заходишь в папку _layouts. Копируешь (Ctrl+C) page.html.

Создаёшь папку _layouts в username.github.io. Вставляешь (Ctrl+V). Редактируешь page.html с помощью [Notepad++](https://notepad-plus-plus.org/downloads/). Удаляешь

```
 class="post-title"
```
<br>

#### Указание источника в постах

Иногда я "репощу" некоторые тексты в моих постах. Я предпочитаю указывать источник текста перед текстом. Дефолтный макет постов помещает заглавие наверху, так что я скопировал post.html в папку _layout и удалил кусок кода, который создаёт заглавие.
 
Markdown файл таких постов выглядит так:

```
---
layout: post
tag: Reposts
comments: true
title: Заглавие текста
---

Источник: [Название источника](ссылка на источник)
<br><br>

# Заглавие текста
```
<br>

#### Комментарии

<https://help.disqus.com/en/articles/1935528-jekyll-installation-instructions>
<br><br>

#### Подчёркивания и заметки на полях

Есть способ воспроизвести подчёркивания и заметки на полях как в бумажных книгах в постах.


```
<span class="underlining">текст</span> <span class="marginalia">комментарий</span>
```

Добавь этот скрипт в post.html:

```
  <style>
    .post-content {
      position: relative;
    }

    .marginalia {
      position: absolute;
      right: -250px;
      width: 200px;
      padding: 10px;
      background-color: #f8f9fa;
      border-left: 3px solid #dee2e6;
      border-radius: 4px;
      font-size: 0.9em;
      color: #000000;
      opacity: 0;
      transform: translateX(20px);
      transition: all 0.3s ease;
      margin-top: -10px;
    }

    .marginalia.visible {
      opacity: 1;
      transform: translateX(0);
    }

    .toggle-annotations {
      position: fixed;
      top: 20px;
      right: 20px;
      padding: 8px 16px;
      background-color: #007bff;
      color: white;
      border: none;
      border-radius: 4px;
      cursor: pointer;
      transition: background-color 0.2s;
      z-index: 1000;
    }

    .toggle-annotations:hover {
      background-color: #0056b3;
    }

    .underlining {
      text-decoration: none;
      transition: text-decoration 0.3s ease;
    }

    .underlining.visible {
      text-decoration: underline;
      text-decoration-color: blue;
      text-decoration-thickness: 3px;
	  text-underline-offset: 5px;
    }

    @media (max-width: 1200px) {
      .toggle-annotations {
        display: none;
      }
    }
  </style>

  <script>
    window.addEventListener('DOMContentLoaded', function() {
      const marginalia = document.querySelectorAll('.marginalia');
      const button = document.getElementById('annotationsButton');
      
      if (marginalia.length > 0) {
        button.style.display = 'block';
      }
    });

    let annotationsVisible = false;

    function toggleAnnotations() {
      const marginalia = document.querySelectorAll('.marginalia');
      const underlinedText = document.querySelectorAll('.underlining');
      const button = document.querySelector('.toggle-annotations');
      
      annotationsVisible = !annotationsVisible;
      
      marginalia.forEach(note => {
        note.classList.toggle('visible', annotationsVisible);
      });

      underlinedText.forEach(text => {
        text.classList.toggle('visible', annotationsVisible);
      });

      button.textContent = annotationsVisible ? 'Hide Annotations' : 'Show Annotations';
    }
  </script>
```