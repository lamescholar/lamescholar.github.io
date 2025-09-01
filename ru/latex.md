---
layout: page
comments: true
title: LaTeX
---

LaTeX - инструмент для вёрстки, с помощью которого можно сделать PDF-файл со сложной математической нотацией.
<br><br>

MiKTeX - <https://miktex.org/download>

TeXstudio - <https://www.texstudio.org/>

<https://rutracker.org/forum/viewtopic.php?t=6191459>

Параметры->Конфугурация TeXstudio...->Компиляция->Просмотрщик PDF->Внешний просмотрщик PDF.

Параметры->Конфугурация TeXstudio...->Команды->Внешний просмотрщик PDF. Укажи путь к Sumatra PDF.
<br><br>

Установи пакет cm-super в MiKTeX Сonsole.

Структура документа:

```
\documentclass[a4paper, 12pt]{article}
\usepackage[margin = 2cm]{geometry}
\usepackage[utf8]{inputenc}
\usepackage[russian]{babel}
\usepackage{amsmath}
\usepackage{tikz}
\usepackage{graphicx}
\usepackage{hyperref}
\hypersetup{colorlinks = true}

\begin{document}
	\sloppy
	
	Hello, World!
\end{document}
```

или

```
Параметры->Конфугурация TeXstudio...->Компиляция->Компилятор по умолчанию->XeLaTeX.
Структура документа:
\documentclass[a4paper, 12pt]{article}
\usepackage[margin = 2cm]{geometry}
\usepackage[utf8]{inputenc}
\usepackage[russian]{babel}
\usepackage{fontspec}
\setmainfont{Times New Roman}
\usepackage{amsmath}
\usepackage{tikz}
\usepackage{graphicx}
\usepackage{hyperref}
\hypersetup{colorlinks = true}

\begin{document}
	\sloppy
	
	Hello, World!
\end{document}
```