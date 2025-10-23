---
layout: page
comments: true
title: LaTeX
---

LaTeX is a tool to make PDF files with complex mathematical notation.
<br><br>

MiKTeX - <https://miktex.org/download>

TeXstudio - <https://www.texstudio.org/>

<https://overleaf.com/learn>

Options->Configure TeXstudio...->Build->PDF Viewer->External PDF Viewer.

Options->Configure TeXstudio...->Commands->External PDF Viewer. Set Sumatra PDF path.
<br><br>

Install cm-super package in MiKTeX Console.

Document structure:

```
\documentclass[a4paper, 12pt]{article}
\usepackage[margin = 2cm]{geometry}
\usepackage[utf8]{inputenc}
\usepackage[english]{babel}
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

or

```
Options->Configure TeXstudio...->Build->Default Compiler->XeLaTeX.
Document structure:
\documentclass[a4paper, 12pt]{article}
\usepackage[margin = 2cm]{geometry}
\usepackage[utf8]{inputenc}
\usepackage[english]{babel}
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