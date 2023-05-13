**Internet Archive**<br/><br/>

<https://github.com/MiniGlome/Archive.org-Downloader><br/><br/>

With that Python script you can rip a book from Internet Archive. Script uses 1 hour loan to download pages of the book. To convert images to PDF script is using img2pdf package. But it creates too big PDF file. So I recommend you to keep -j setting at the end of the command to get only the images. Three options how you can efficiently convert them into PDF or DjVu follow.<br/><br/>

Requirements to install:

Git - <https://git-scm.com/download/win>

Python - <https://www.python.org/downloads/>

Tick Add python.exe to PATH while downloading Python.<br/><br/>

Installation:

```
Win+R
cmd
cd C:\
git clone https://github.com/MiniGlome/Archive.org-Downloader.git
cd Archive.org-Downloader
pip install -r requirements.txt
```
<br/><br/>
To use you need to register.

<https://archive.org/account/signup><br/><br/>

Usage:

```
Win+R
cmd
cd C:\Archive.org-Downloader
python archive-org-downloader.py -e email -p password -r 0 -u https://archive.org/details/untoldhistoryoft00ston -j
```
<br/><br/>
Pictures are downloaded without a certain DPI. Because of this, there may be problems when creating a file. DPI can be set using the IrfanView program.

In addition to DPI fix, if the scans are dark and the text is faded, you can use Contrast and Gamma correction color correction tools in the Irfan View program. I use the following grid of values (the first column is Contrast, the second is Gamma correction):

90 4.00

70 3.00

50 2.00

30 1.50

These are the values for the case when the scan is dark and it needs to be brightened. If the standard options are not suitable, you need to experiment with different combinations - Shift+G. Visually Contrast makes the text bold, brightens the background. Gamma correction lightens of the scan, but bleach the text. Useful combinations: 70 2.00 (the scan is not very dark, there is greenish or orange tint), only Contrast - 50/70 (the scan is not very dark, the text is faded), 50 0.75 (the scan is quite light, the text is faded), only Gamma correction - 0.62 (the scan is very light).

If there is greenish or orange tint remaining, you can lower the color saturation of the scan. Saturation tool is used for this. The value is -100/-150.

In addition to color correction tools, Sharpen tool is very often useful. It is used in the presence of blurred text (photography defect). The optimal value is 30.<br/><br/>

Fix DPI:

IrfanView - <https://www.irfanview.com/>

File->Batch Conversion/Rename...

Add images. Sort files. By Name. Auto sort file list after insert. Add all.

Output format:->JPG

Use advanced options (for bulk resize...)->Advanced->Save new DPI value: 300 or 600. Enter the values of Gamma correction, Constrast, and Saturation, if necessary. Sharpen: 30, if necessary.

Choose output folder.

Start Batch.<br/><br/>

JPG to PDF:

LuraTech PDF Compressor - <https://archive.org/details/LuraTechPDFCompressorDesktopV6.2.0.4>

Options:

Profile: Standart

Quality: 9

or

Profile: Photo

Quality: 6<br/><br/>

or<br/><br/>

JPG to PDF:

Adobe Acrobat XI Pro - <https://rutracker.org/forum/viewtopic.php?t=5480244>

Create->Combine Files into a Single PDF...->Always add bookmarks to Adobe PDF. Untick.

Add Files...->Add Files...->Combine Files.

Tools->Text Recognition->In This File->Edit..

Pick corresponding language.

PDF Output Style: ClearScan

300 dpi

File->Save.<br/><br/>

or<br/><br/>

JPG to DjVu:

Image processing in Scan Tailor.

If width of image is greater than 2000 - 300 DPI, greater than 2000 - 600 DPI.

Look [DjVu](https://lamescholar.github.io/en/djvu).<br/><br/>

Don't forget to delete folders with images.<br/><br/>

Publish your book:

Library Genesis - <https://library.bz/main/upload/>

genesis

upload

RuTracker - <http://rutracker.org/forum/index.php>