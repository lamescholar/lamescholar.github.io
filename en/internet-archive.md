---
layout: page
comments: true
title: Internet Archive
---

<https://github.com/MiniGlome/Archive.org-Downloader>
<br><br>

With this Python script you can download any book from Internet Archive. The script downloads the pages of the book. To convert images to PDF, the script uses img2pdf package. But it creates too big PDF file. So I recommend you to keep -j setting to get only the images. Further I list three options how you can efficiently convert them into PDF or DjVu.
<br><br>

#### Requirements to install:

Git - <https://git-scm.com/download/win>

Python - <https://www.python.org/downloads/>

Tick Add python.exe to PATH while downloading Python.
<br><br>

#### Installation:

Win+R cmd

```
cd C:\
git clone https://github.com/MiniGlome/Archive.org-Downloader.git
cd Archive.org-Downloader
pip install -r requirements.txt
pip install pycryptodome
```
<br>

To use you need to register:

<https://archive.org/account/signup>

If you have bad eyesight, you can get access to all books and [microfilms](https://archive.org/details/sim_microfilm?and%5B%5D=mediatype%3A%22collection%22):

<https://docs.google.com/forms/d/e/1FAIpQLScSBbT17HSQywTm-fQawOK7G4dN-QPbDWNstdfvysoKTXCjKA/viewform>
<br><br>

#### Downloading images:

Win+R cmd

```
cd C:\Archive.org-Downloader
python archive-org-downloader.py -j -e email -p password -r 0 -u https://archive.org/details/untoldhistoryoft00ston
```
<br>

On this stage you can process images in Scan Tailor and encode them into DjVu file with DjVu Small Mod.

See [DjVu](/en/djvu).

Or you can do a color correction and encode images into PDF.
<br><br>

#### Color correction

If the scans are dark and the text is faded, you can use Contrast and Gamma correction color correction tools in the IrfanView program. I use the following grid of values (the first column is Contrast, the second is Gamma correction):

90 4.00

70 3.00

50 2.00

These are the values in case the scan is dark and it needs to be brightened. If the standard options are not suitable, you need to experiment with different combinations - Shift+G. Visually Contrast makes the text bold and brightens the background. Gamma correction lightens of the scan, but bleach the text.

Useful combinations:<br>
70 2.00 (the scan is not very dark, there is greenish or orange tint),<br>
50/70 (the scan is not very dark, the text is faded),<br>
50 0.75 (the scan is quite light, the text is faded),<br>
0.62 (the scan is very light),<br>
90 6.99 (the scan is very dark).

If there is greenish or orange tint remaining, you can lower the color saturation of the scan. Saturation tool is used for this. The value is -100/-150.

It is better to apply color correction to the cover separately. Often a combination of 50/70 2.00 is suitable, sometimes just 2.00 when the photo is very dark.

In addition to color correction tools, I use Sharpen tool all the time against blurred text. The optimal value is 30.

Script download pictures without a certain DPI. Because of this, there may be problems when creating a file. DPI is set in the same IrfanView program.

IrfanView - <https://www.irfanview.com/>

Open a page of the book.

File->Batch Conversion/Rename...

Add images. Sort files. By Name. Auto sort file list after insert. Add all.

Output format:->JPG

Use advanced options (for bulk resize...)->Advanced->Save new DPI value: 300 or 600. If width of image is less than 2000 - 300 DPI, greater than 2000 - 600 DPI. In the case of LuraTech PDF Compressor 300 DPI is not necessary to set - this is the default value when DPI is not set. Enter the values of Gamma correction, Constrast, Saturation, Sharpen, if necessary.

Choose output folder.

Start Batch.
<br><br>

#### Encoding images into PDF file:

**Option №1:**

LuraTech PDF Compressor - <https://archive.org/details/LuraTechPDFCompressorDesktopV6.2.0.4>

Options:

Profile: Standard

Quality: 9

<sup>Standard.</sup>

or

Profile: Photo

Quality: 7

<sup>If you want to preserve the quality of pictures.</sup>

or

Profile: B/W

Quality: 10

<sup>If the book got no pictures. In this scenario there's no need for color correction, except the cover. You can add the cover to B/W document with [PDF-XChange](https://rutracker.org/forum/viewtopic.php?t=6601303) (look out for bookmarks).</sup>

**Option №2:**

Adobe Acrobat XI Pro - <https://rutracker.org/forum/viewtopic.php?t=5160028>

Create->Combine Files into a Single PDF...->Options->Always add bookmarks to Adobe PDF. Untick.

Add Files...->Add Files...->Combine Files.

Tools->Text Recognition->In This File->Edit..

Pick corresponding language.

PDF Output Style: ClearScan

300 dpi

File->Save.
<br><br>

There is an alternative to PDF, if no matter the manipulations you get drastic quality loss. You can zip the folder with images and change the file extention to .cbz. You can open CBZ file with [Sumatra PDF](https://www.sumatrapdfreader.org/download-free-pdf-viewer). The obvious downside - no compression. Another one - no OCR.
<br><br>

Don't forget to delete folders with images.
<br><br>

#### Publish your book:

Library Genesis - <https://library.bz/main/upload/><br>
genesis<br>
upload

RuTracker - <http://rutracker.org/forum/index.php>

VK - <https://vk.com/docs>