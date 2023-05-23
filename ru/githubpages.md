**Пособие по созданию статического сайта**<br/><br/>

С помощью Github Pages можно создать бесплатный статический сайт для своего блога или библиотеки. Лимит совокупного размера файлов сайта - 1 ГБ.<br/><br/>

**Создание сайта**

<https://docs.github.com/ru/pages/setting-up-a-github-pages-site-with-jekyll/creating-a-github-pages-site-with-jekyll><br/><br/>

**Информация на сайте**

Прописываешь в файле _config.yml название сайта, электронную почту, описание (его можно удалить). В файле about.markdown прописываешь описание сайта.

**Создание страницы**

Создай .md файл в папке сайта. Например, page.md. Тогда на твоём сайте появится страничка по адресу https://nickname.github.io/page. Можешь поместить файл в папку folder.  Тогда на твоём сайте появится страничка по адресу https://nickname.github.io/folder/page<br/><br/>

**Форматирование**

Жирный текст - <div>**жирный текст**</div>. Курсив - <div>*курсив*<div>. Новый абзац - пустая строка. Двойной отступ - <div><br/><br/></div> в конце абзаца. Для отображения пробелов смотри <https://stackoverflow.com/questions/44810511/how-to-add-empty-spaces-into-md-markdown-readme-on-github>. Для отключения форматирования смотри <https://stackoverflow.com/questions/701042/disable-markdown-for-a-block>. Выделение ссылки - <div><ссылка></div>. Ссылка - <div>[текст](ссылка)</div>. Выделение кода - <div>```</div>.<br/><br/>

**Добавление картинки**

Допустим, ты положил картинку image.png в папку images. Чтобы отобразить её на странице пропиши

```
{:refdef: style="text-align: center;"}
![Описание картинки](/images/image.png)
{: refdef}
```

Чтобы добавить ссылку к картинке пропиши

```
{:refdef: style="text-align: center;"}
[![Описание картинки](/images/image.png)](ссылка)
{: refdef}
```

**Добавление иконки сайта**

<https://medium.com/@xiang_zhou/how-to-add-a-favicon-to-your-jekyll-site-2ac2179cc2ed>