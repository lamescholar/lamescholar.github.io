**Пособие по созданию статического сайта**<br/><br/>

С помощью Github Pages можно создать бесплатный статический сайт для своего блога или библиотеки. Лимит совокупного размера файлов сайта - 1 ГБ.<br/><br/>

Создание сайта

<https://docs.github.com/ru/pages/setting-up-a-github-pages-site-with-jekyll/creating-a-github-pages-site-with-jekyll><br/><br/>

Информация на сайте

Прописываешь в файле _config.yml название сайта, электронную почту, описание (его можно удалить). В файле about.markdown прописываешь описание сайта.<br/><br/>

Создание страницы

Создай .md файл в папке сайта. Например, page.md. Тогда на твоём сайте появится страничка по адресу https://nickname.github.io/page. Можешь поместить файл в папку folder.  Тогда на твоём сайте появится страничка по адресу https://nickname.github.io/folder/page<br/><br/>

Форматирование

<pre>
Жирный текст - **жирный текст**. Курсив - *курсив*. Новый абзац - пустая строка. Двойной отступ - <br/><br/> в конце абзаца. Выделение ссылки - <ссылка>. Ссылка - [текст](ссылка). Выделение кода - ```.
</pre>

Для отключения форматирования смотри <https://stackoverflow.com/questions/701042/disable-markdown-for-a-block>. Для создания блока кода смотри <https://docs.github.com/ru/get-started/writing-on-github/working-with-advanced-formatting/creating-and-highlighting-code-blocks><br/><br/>

Добавление картинки

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
<br/><br/>
Добавление иконки сайта

<https://medium.com/@xiang_zhou/how-to-add-a-favicon-to-your-jekyll-site-2ac2179cc2ed><br/><br/>

Обновление сайта

```
Win+R
cmd
cd nickname.github.io
git add .
git commit -a
git push
```

Строчка git add . нужна в случае добавления новых файлов. После ввода строчки git commit -a в командной строке появится текстовый редактор. Нажимаешь i. Стрелочками перемещаешь курсор. Стираешь решётки у нужных строк.

```
Esc
:wq
Enter
```
