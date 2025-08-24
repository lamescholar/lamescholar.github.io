---
comments: true
title: Jekyll
---

Using [Jekyll](https://jekyllrb.com/) (static site generator) and [GitHub Pages](https://pages.github.com/) (hosting that runs Jekyll), you can create a free static site for your blog. The size limit is 1 GB.
<br><br>

To create a site you need to register on GitHub:

<https://github.com/>
<br><br>

To create a site you need to install:

Git - <https://git-scm.com/download/win>

Jekyll - <https://jekyllrb.com/docs/installation/windows/>
<br><br>

#### Creating a site

Instead of username use your GitHub username.

Go to the command line:

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

Your site will be located at https://username.github.io/

Source: <https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/creating-a-github-pages-site-with-jekyll>
<br><br>

#### Information on the site

In the _config.yml file fill title, author, email, url, description (you can delete it). In the about.markdown file, write a description of the site.
<br><br>

#### Creating a page

Create a .md file in the site folder. For example, page.md . Then a page will appear on your site at https://username.github.io/page. You can put the file in the folder named folder. Then a page will appear on your site at https://username.github.io/folder/page.
<br><br>

#### Creating a post

<https://jekyllrb.com/docs/posts/>
<br><br>

#### Formatting

```
1) Bold text - **bold text**
2) Italics - *italics*
3) Title (in the beginning of the text):
---
comments: true
title: Title
---
4) Heading - # heading text
5) Subheading - #### subheading text
6) New paragraph - empty line
7) Highlight a link - <link>
8) Link - [text](link)
9) Link to site page - [text](/folder/page)
10) Link back and forth:
text<a href="#note" id="note-back">†</a>

<a href="#note-back" id="note">†</a> text of the note
11) Link to place in text:
[Place](#place)

<a id="place"></a>
12) Table of Contents:
#### Table of Contents
[Introduction](#introduction)

<a id="introduction"></a>
#### Introduction
13) Line break - <br>
14) Blank line (double line break) - <br><br>
15) Note:
text[^1] text[^2]

[^1]: note text

	note text

[^2]: note text
16) Quote:
> quote
>
> the rest of quote
17) Small text - <sub>text</sub>
```

Code block - <https://docs.github.com/ru/get-started/writing-on-github/working-with-advanced-formatting/creating-and-highlighting-code-blocks>

<https://www.markdownguide.org/basic-syntax/>
<br><br>

#### Adding picture

Let's say you put an image.png picture in the folder named images.

Place an image on the page:

```
![Picture description](/images/image.png)
```

In the center:

```
{:refdef: style="text-align: center;"}
![Picture description](/images/image.png)
{: refdef}
```

With a link:

```
{:refdef: style="text-align: center;"}
[![Picture description](/images/image.png)](link)
{: refdef}
```
<br>

#### Adding audio

<https://stackoverflow.com/questions/63701944/how-to-embed-audio-into-a-jekyll-blog>
<br><br>

#### Adding video

<https://github.com/nathancy/jekyll-embed-video>

<https://stackoverflow.com/questions/48876911/embedded-local-mp4-not-playing-in-chrome-when-running-jekyll-serve-econnreset>
<br><br>

#### Adding a site icon

<https://medium.com/@xiang_zhou/how-to-add-a-favicon-to-your-jekyll-site-2ac2179cc2ed>
<br><br>

#### Updating the site

Win+R cmd

```
cd username.github.io
git add .
git commit -m "new commit"
git push
```

You can create .bat file and put these commands into it. Then the commit can be done with two clicks. To prevent the command line from closing immediately after executing commands, add pause command.
<br><br>

#### Starting the site locally

To counter an error,  you need to add webrick to Gemfile:

```
cd username.github.io
bundle add webrick
```

Starting the site:

```
cd username.github.io
bundle exec jekyll serve
```

Open given address.
<br><br>

#### Navigation area filtration (upper right corner)

Paste in _config.yml:

```
header_pages:
  -about.markdown
```
<br>

#### Changing title size

Go to minima folder. On Windows it is located somewhere here:

C:\Ruby32-x64\lib\ruby\gems\3.2.0\gems\minima-2.5.1

Go to _layouts folder. Copy (Ctrl+C) page.html.

Create _layouts folder in username.github.io. Paste (Ctrl+V). Edit page.html with [Notepad++](https://notepad-plus-plus.org/downloads/). Remove

```
 class="post-title"
```
<br>

#### Stating a source in posts

Sometimes I "repost" some texts in my posts. I prefer to state a source of the text in front of the text. Default post layout puts the title at the top, so I copied post.html into _layout folder and removed piece of code that create title.
 
Markdown file of such posts looks like this:

```
---
layout: post
tag: Reposts
comments: true
title: Title of the text
---

Source: [Source title](link to the source)
<br><br>

# Title of the text
```
<br>

#### Comments

<https://help.disqus.com/en/articles/1935528-jekyll-installation-instructions>
<br><br>

#### Underlinings and marginalia

There is a way to reproduce in posts the underlinings and marginalia as in printed books.


```
<span class="underlining">text</span> <span class="marginalia">comment</span>
```

Add this script to post.html:

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
	  text-underline-offset: 4px;
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