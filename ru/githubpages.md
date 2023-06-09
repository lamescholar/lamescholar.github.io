**Github Pages**<br/><br/>

С помощью Github Pages можно создать бесплатный статический сайт для своего блога или библиотеки. Лимит совокупного размера файлов сайта - 1 ГБ.<br/><br/>

Для создания сайта необходимо зарегистрироваться на Github:

<https://github.com/><br/><br/>

Для создания сайта необходимо установить:

Git - <https://git-scm.com/download/win>

Jekyll - <https://jekyllrb.com/docs/installation/windows/><br/><br/>

Создание сайта

Создай репозиторий с названием username.github.io (вместо username использую твой username на Github).

Теперь отправляйся в командную строку:

```
Win+R
cmd
git init username.github.io
cd username.github.io
git checkout --orphan main
git rm -rf .
jekyll new --skip-bundle .
bundle install
git add .
git commit -m 'Initial GitHub pages site with Jekyll'
git remote add origin https://github.com/username/username.github.io.git
git push -u origin main
```

Твой сайт будет расположен по адресу https://username.github.io/<br/><br/>

Информация на сайте

Прописываешь в файле _config.yml название сайта, электронную почту, описание (его можно удалить). В файле about.markdown прописываешь описание сайта.<br/><br/>

Создание страницы

Создай .md файл в папке сайта. Например, page.md. Тогда на твоём сайте появится страничка по адресу https://username.github.io/page. Можешь поместить файл в папку folder.  Тогда на твоём сайте появится страничка по адресу https://username.github.io/folder/page.<br/><br/>

Форматирование

```
Жирный текст - **жирный текст**.
Курсив - *курсив*.
Новый абзац - пустая строка.
Выделение ссылки - <ссылка>.
Ссылка - [текст](ссылка).
Двойной отступ - <br/><br/>.
Сноска:
текст[:1] текст[:2]

[:1]: текст сноски

	текст сноски

[:2]: текст сноски
```

<https://www.markdownguide.org/basic-syntax/><br/><br/>

Создание блока кода - <https://docs.github.com/ru/get-started/writing-on-github/working-with-advanced-formatting/creating-and-highlighting-code-blocks>.<br/><br/>

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
Ссылка на документ

Допустим, ты положил документ Nagel T. - What Does It All Mean__ A Very Short Introduction to Philosophy - 1987.epub в папку с названием doc. Чтобы сделать ссылку на этот документ пропиши

```
[What Does It All Mean?](/doc/Nagel T. - What Does It All Mean__ A Very Short Introduction to Philosophy - 1987.epub)
```
<br/><br/>
Добавление иконки сайта

<https://medium.com/@xiang_zhou/how-to-add-a-favicon-to-your-jekyll-site-2ac2179cc2ed><br/><br/>

Обновление сайта

```
Win+R
cmd
cd username.github.io
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