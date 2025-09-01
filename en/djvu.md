---
layout: page
comments: true
title: DjVu
---

This is comprehensive collection of programs to create, edit and read DjVu files. Using it you can create ebook in DjVu format with OCR layer (text layer) and contents.
<br><br>

#### General algorithm:

1) Scan Tailor Universal - images processing.

2) Book Restorer - straightening text lines.

3) Tsushima - cleaning slur.

4) DjVu Small Mod 0.7.6.1 - creation of DjVu document.

5) DjVu Imager - inserting colored/grey pictures.

6) ABBYY Finereader - creation of OCR layer.

7) FR11 DjVu Text Layer Crutch - fixing and transferring OCR layer.

8) Document Express Editor 6.0.1 - adding a cover.

9) Pdf & DjVu Bookmarker - adding a contents.

10) DjVu Hyperlinks Editor - adding hyperlinks.

11) DjVu Annotations Editor - editing style of hyperlinks.

12) Document Express Editor 6.0.1 - editing hyperlinks.
<br><br>

**WinDjView** - program for reading of .djvu files.

Alt+Left - go back after clicking on the hyperlink.

Ctrl+M - change the scale. If pre-installed scales 150% and 200% don't suit, choose arithmetic mean - 175%, if this doesn't suit, then 162% or 187%. If you need the scale little greater than 150% - add 6%.

If you have blurry image, you need to follow Properties->Compatibility->Change high DPI settings->Change settings for all users->Override high DPI scaling behaviour. Scaling performed by:->Application.

<https://windjview.sourceforge.io/>
<br><br>

**IrfanView** - program for converting images.

<https://www.irfanview.com/64bit.htm>
<br><br>

**Scan Tailor Universal** - program for images processing.

Settings:<br>
General->Ask every time. Untick.<br>
General->Thumbnails panel->Scale cashed images to this size: 1000 px<br>
General->Tiff compression->TIFF compression (b/w): CCIITTFAX4<br>
Page layout->Margins. 10 everywhere.<br>
Page layout->Alignment->Auto-Magnet alignment. Tick.<br>
Output->Hold spacebar to display original page. Tick.<br>
Output->Mixed mode->Foregroud layer. Untick.

New Project... Select a folder with pictures. Then you can remove some pictures from the project, for example, the cover.

To enlarge miniatures, press Alt and scroll.

For comfortable navigation between minatures use keys pgup and pgdn.

**Processing:**

1) Fix Orientation

Rotatation of pages on 90 degrees. To apply to a group of pictures, click Apply to... Select the scope.

2) Split Pages

If there is a piece of another page in the pictures or two pages in the pictures, start. The program will either crop the picture or split it into two. Just in case, it is better to check behind the program and view the result on thumbnails.

3) Deskew

Text skew correction.

4) Select Content

The program automatically finds the content of the page - throws a rectangle on the page, the content of which will be taken into the final image. Again, launch and then check for the program and, in case of inaccuracy, correct it manually.

5) Page Layout

If the content rectangle is small, the margins can be 5 mm. If you process images with the cover, you need to make zero margins for the cover and uncheck Match size with other pages.

6) Output

Look at the result of binarization. If parts of the letters disappear - set the Binarization threshold to 20. In extreme cases - 30. An increased Binarization threshold adds boldness to the text. If the book got pictures, you must use the Mixed mode. Untick Auto layer. Tick Picture zone layer. Untick Equalize illumination, if pictures lose details. Let's run the output. The program will automatically find pictures. After the output you need to check behind the program. Look through all the pages with pictures. In the same time you are looking for spots on pages that can be deleted in Fill Zones section. If the picture zone was found incorrectly, you need to correct it. You need to go to the Layers section. Either drag vertices. Or delete the zone and create your own. You right-click on the picture, hold down Ctrl to make the area rectangular and draw a rectangle. If the zone has a complex shape, you make a polygon. The picture zone can be used on a part of the picture where the text is poorly recognized (text details will disappear during binarization). Split text and images. Tools->Export...->Export. After processing the images, save the project.

<http://forum.ru-board.com/topic.cgi?forum=5&topic=32945>
<br><br>

**Book Restorer** - program for straightening crooked images. Create Book. If necessary, you can leave the original file names: Standart page->Properties->Numbering->Original name. Select all files (Ctrl+A). Tools->Restore->Geometrical correction. Publish (icon of disk in menu). When straightening bitonal images in column Types of files choose G4-compressed, in column Color range - Binary. Check the result. If the result is more crooked than original image, substitute the result with original image. When straightening text of the book with pictures, you need to input into the program colored images you got from Scan Tailor. TIFF LZW compressed, Color range - RGB colors.

<http://djvu-converter.narod.ru/><br>
<https://archive.org/details/book-restorer-v.-4.2.1>
<br><br>

**Tsushima** - program for clearing slur. Drag images to program icon. Result - images in 8BPP 96DPI format. Convert images to 1BPP 600DPI format in IrfanView.

<http://publ.lib.ru/cgi/forum/YaBB.pl?num=1530528723/13#13>
<br><br>

**DjVu Small Mod 0.7.6.1** - program for encoding and decoding DjVu documents, in other words, for creating DjVu documents out of images and extracting images out of DjVu documents. For bitonal images use following encoding profile:

Profile set: Original

Type: Bitonal

DPI: 600

<https://book-scan.wixsite.com/djvu/blank-z8lfg>
<br><br>

**DjVu Imager** - program for inserting pictures. Set path to DjVu document with pictures cutted-out and path of output document. Set the path to out/export/pic folder. Convert. Insert in DjVu. Now you got DjVu document with pictures. Settings: BSF - 2, DPI - 300.

<http://www.djvu-soft.narod.ru/scan/djvu_imager_en.htm>
<br><br>

**FSD** - alternative to DjVu Small Mod + DjVu Imager.

<http://www.djvu-soft.narod.ru/soft/>

<https://www.youtube.com/watch?v=jOQBTV-zvts>
<br><br>

DjVu Small Mod + DjVu Imager and FSD realize the method of separated scans. The images are separated into text and pictures, that encoded separately.
<br><br>

**Document Express Editor 6.0.1** - program for deleting/adding images into DjVu document. Used for adding a cover. If a line appear in expanded window, use compatibility settings as described for WinDjView.

<http://www.djvu-soft.narod.ru/soft/>
<br><br>

**ABBYY Finereader** - program for adding OCR layer. You can use the program to extract tif files from PDF-document. Options->Images processing, tick No preprocessing, so OCR layer lies in place. Thorough recognition is necessary. You need only text layer out of output document, so to quicken output, you can set DjVu export settings with maximum compression.

<https://btdig.com/db98398f6d1c9bbd4c8ac905dc30abb5f9e4b704/abbyy-finereader-kpojiuk>
<br><br>

**FR11 DjVu Text Layer Crutch** - program for fixing OCR layer in Finereader output DjVu document and transferring it in initial DjVu document (in Finereader output DjVu document colored/grey pictures lose quality).

<https://forum.ru-board.com/topic.cgi?forum=5&topic=38467>
<br><br>

**DjVu Clean Page Inserter** - program for inserting empty pages into DjVu document.

<https://forum.ru-board.com/topic.cgi?forum=5&topic=38467>
<br><br>

**Pdf & DjVu Bookmarker** - program for adding contents. Copy text of contents. Insert in the program. Edit. You can arrange Bookmarks in a hierarchy. Insert into DjVu document. Pay your attention to F2 и F3 keys, they quicken work considerably.

<https://sourceforge.net/projects/djvubookmarker/>
<br><br>

**DjVu Hyperlinks Editor** - program for automatic creation of hyperlinks. OCR layer is required. As Shift set difference between number of document page and number of book page. Then set document pages of contents / alphabetic index. Choose Job type Content / Alphabetic index 2. Now you got 'hyperlinks, apparent with pointing of cursor on elements of contents' / 'hyperlinks in alphabetic index'.

<http://www.djvu-soft.narod.ru/soft/>
<br><br>

**DjVu Annotations Editor** - program for changing properties of hyperlinks. Go to Свойства гиперссылок. Choose Отображать постоянно (if you're changing hyperlinks of alphabetic index), set off Заливка и delete Комментарий. Применить. Сохранить. Open DjVu document in Document Express Editor 6.0.1 program and delete hyperlinks on page numbers - Annotation->Delete. To delete/add hyperlinks of contents by hands you need to click Select Annotations in menu - hyperlinks of contents will become apparent. Then, for example, you can edit hyperlink borders, which overlapped several elements of contents and create absent hyperlink by clicking Rectangular Hyperlink in menu and selecting element of contents. In option Style choose Plain Border, Persistent, in option Link - Page Number, in option Page – page of document.

<https://forum.ru-board.com/topic.cgi?forum=5&topic=38467>
<br><br>

**DjVu Chunk Remover** - program for deleting chunks, pages in DjVu document.

<https://forum.ru-board.com/topic.cgi?forum=5&topic=38467>
<br><br>

Zip-archive with programs in case the links break:<br>
[DjVu.zip](/files/DjVu.zip)<br>
<https://disk.yandex.ru/d/odtW8TX4diIVsg>
<br><br>

#### Publish your book:

Library Genesis:<br>
<https://library.bz/main/upload/><br>
genesis<br>
upload<br>
<https://libgen.li/librarian.php>

Z-Library - <https://singlelogin.re/book-add>

RuTracker - <https://rutracker.org/forum/index.php>

VK - <https://vk.com/docs>
<br><br>

#### Information:

<http://www.djvu-soft.narod.ru/>

<http://publ.lib.ru/cgi/forum/YaBB.pl>