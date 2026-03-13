---
layout: post
tag: Posts
comments: true
title: How to listen to German radio
---

2026-03-13

# How to listen to German radio
<br>

Now is a golden age of language learning. Small language models are lightweight and free, your laptop can run them. These models can transcribe and translate European languages to English. You can download MP3 file of [Deautchlandfunk Kultur](https://www.deutschlandfunkkultur.de/) broadcast, transcribe it with [whisper](/en/whisper), translate it with [Qwen3-4B](/en/machine-translation), build a PDF with transcript and translation. Now you can listen to broadcast, see the transcript and translation, pause, go back ([Winamp](https://sourceforge.net/projects/winamp/) has global hotkeys), look up a word in the [dictionary](/en/dictionaries).

PDF script to combine transcript and translation:

```
import nltk
from fpdf import FPDF
from nltk.tokenize import sent_tokenize

# setup
nltk.download('punkt')
pdf = FPDF()
pdf.set_auto_page_break(auto=True, margin=15)
pdf.add_page()

# font
pdf.add_font("Arial", style="", fname="C:/Windows/Fonts/arial.ttf")
pdf.set_font('Arial', size=11)

# layout
margin = 15
gutter = 10
col_width = (pdf.w - (margin * 2) - gutter) / 2
line_height = 6

def get_sentences(file_path):
    with open(file_path, "r", encoding="utf-8") as f:
        return sent_tokenize(f.read())

left_sentences = get_sentences("text.txt")
right_sentences = get_sentences("translation.txt")

for left_txt, right_txt in zip(left_sentences, right_sentences):
    # calculate the height needed for both sides
    # split_lines() helps us predict how many lines fpdf will create
    lines_left = pdf.multi_cell(col_width, line_height, left_txt, split_only=True)
    lines_right = pdf.multi_cell(col_width, line_height, right_txt, split_only=True)
    
    max_lines = max(len(lines_left), len(lines_right))
    row_height = max_lines * line_height + 4 # +4 for internal padding

    # check for page break
    if pdf.get_y() + row_height > pdf.page_break_trigger:
        pdf.add_page()

    start_x = pdf.get_x()
    start_y = pdf.get_y()

    # draw the border
    pdf.rect(start_x, start_y, pdf.w - (margin * 2), row_height)
    
    # draw the middle line
    pdf.line(start_x + col_width + (gutter/2), start_y, 
             start_x + col_width + (gutter/2), start_y + row_height)

    # place the text
    pdf.set_xy(start_x + 2, start_y + 2) # +2 for padding inside box
    pdf.multi_cell(col_width, line_height, left_txt, border=0, align='L')
    
    pdf.set_xy(start_x + col_width + gutter, start_y + 2)
    pdf.multi_cell(col_width, line_height, right_txt, border=0, align='L')

    # move cursor to the bottom of the common box
    pdf.set_y(start_y + row_height)

pdf.output("parallel.pdf")
```