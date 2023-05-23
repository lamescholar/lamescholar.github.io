**Github Pages**<br/><br/>

Using Github Pages, you can create a free static website for your blog or library. The limit of the total size of the site files is 1 GB.<br/><br/>

To create a website you need to register on Github:

<https://github.com/><br/><br/>

To create a website you need to install:

Git - <https://git-scm.com/download/win>

Jekyll - <https://jekyllrb.com/docs/installation/windows/><br/><br/>

Creating a website

Create repository with the name username.github.io (instead of username use your Github username).

Now go to the command line:

```
Win+R
cmd
git clone https://github.com/username/username.github.io
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

Your website will be located at https://username.github.io/<br/><br/>

Information on the website

Write in the _config.yml file the name of the site, email, description (you can delete it). In the about.markdown file, write a description of the site.<br/><br/>

Creating a page

Create a .md file in the site folder. For example, page.md . Then a page will appear on your website at https://username.github.io/page. You can put the file in the folder named folder.  Then a page will appear on your website at https://username.github.io/folder/page.<br/><br/>

Formatting

```
Bold text - **bold text**.
Italics - *italics*.
New paragrapgh - empty line.
Mark out a link - <link>.
Link - [text](link).
Double line break - <br/><br/>.
```

Creating code block - <https://docs.github.com/ru/get-started/writing-on-github/working-with-advanced-formatting/creating-and-highlighting-code-blocks>.<br/><br/>

Adding picture

Let's say you put an image.png picture in the folder named images. To display it on the page, write

```
{:refdef: style="text-align: center;"}
![Picture description](/images/image.png)
{: refdef}
```

To add a link to the picture, write

```
{:refdef: style="text-align: center;"}
[![Picture description](/images/image.png)](link)
{: refdef}
```
<br/><br/>
Link to a document

Let's say you put a document Nagel T. - What Does It All Mean__ A Very Short Introduction to Philosophy - 1987.epub in the folder named doc. To make a link to this document, write

[What Does It All Mean?](/doc/Nagel T. - What Does It All Mean__ A Very Short Introduction to Philosophy - 1987.epub)<br/><br/>

Adding a website icon

<https://medium.com/@xiang_zhou/how-to-add-a-favicon-to-your-jekyll-site-2ac2179cc2ed><br/><br/>

Updating the website

```
Win+R
cmd
cd username.github.io
git add .
git commit -a
git push
```

Line git add .  is needed in case of adding new files. After entering the line git commit -a a text editor will appear on the command line. Enter i. Move the cursor with the arrows. Erase # at the right lines.

```
Esc
:wq
Enter
```