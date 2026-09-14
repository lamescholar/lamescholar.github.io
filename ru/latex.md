---
layout: page
comments: true
title: LaTeX
---

LaTeX - это язык, используемый для вёрстки PDF-файлов со сложной математической нотацией.
<br><br>

Генератор:<br>
MiKTeX - <https://miktex.org/download>

Редактор:<br>
TeXstudio - <https://www.texstudio.org/>

<https://rutracker.org/forum/viewtopic.php?t=6191459>

Параметры->Конфугурация TeXstudio...->Компиляция->Просмотрщик PDF->Внешний просмотрщик PDF.

Параметры->Конфугурация TeXstudio...->Команды->Внешний просмотрщик PDF. Укажи путь к Sumatra PDF.
<br><br>

Структура документа:

```
\documentclass[a4paper, 12pt]{article}
\usepackage[margin = 2cm]{geometry}
\usepackage[T2A]{fontenc}
\usepackage[english, russian]{babel}
\usepackage{parskip}
\usepackage{mlmodern}
\usepackage{amsmath}
\usepackage{tikz}
\usepackage{graphicx}
\usepackage{hyperref}
\hypersetup{colorlinks = true}

\begin{document}
	\sloppy
	
	Привет!
\end{document}
```
