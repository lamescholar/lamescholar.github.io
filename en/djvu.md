DjVu<br/><br/>

This is comprehensive collection of programs to create, edit and read DjVu. Using it you can create ebook in djvu format with OCR layer (text layer) and contents.<br/><br/>

Functions of programs:<br/><br/>

WinDjView - program for reading of .djvu files. Advice for comfortable reading. If pre-installed scales 150% and 200% don't suit, choose arithmetic mean - 175%, if this doesn't suit, then 162% or 187%. If you need the scale little greater than 150% - add 6%. Alt+Left - go back after clicking on the hyperlink. If you have blurry image, you need to follow Properties->Compatibility->Change high DPI settings->Change settings for all users->Override high DPI scaling behaviour. Scaling performed by:->Application.

[https://windjview.sourceforge.io/](https://windjview.sourceforge.io/)<br/><br/>

IrfanView - program for converting images.

[https://www.irfanview.com/](https://www.irfanview.com/)<br/><br/>

Scan Tailor Universal -  - program for images processing.

Settings:

Tools->Settings...->General->Ask every time. Untick. General->Thumbnails panel->Scale cashed images to this size: 1000 px. General->Tiff compression->TIFF compression (b/w): CCIITTFAX4. Page layout->Margins. 10 everywhere. Output->Hold spacebar to display original page. Tick. Output->Mixed mode->Foregroud layer. Untick.

New Project... Select a folder with pictures. Then you can remove some pictures from the project, for example, the cover.

Recommendation. To enlarge miniatures, press Alt and scroll.

Recommendation for comfortable navigation between minatures. You can use keys pgup and pgdn for navigation between pages.

Processing:

1 Fix Orientation

Rotatation of pages on 90 degrees. To apply to a group of pictures, click Apply to... Select the scope.

2 Split Pages

If there is a piece of another page in the pictures or two pages in the pictures, we start. The program will either crop the picture or split it into two. Just in case, it is better to check behind the program and view the result on thumbnails.

3 Deskew

Text skew correction.

4 Select Content

The program automatically finds the content of the page - throws a rectangle on the page, the content of which will be taken into the final image. Again, we launch and then check for the program and, in case of inaccuracy, we correct it manually.

5 Page Layout

If the content rectangle is small, the margins can be 5 mm. If you process images with the cover, you need to make zero margins for the cover and uncheck Match size with other pages.

6 Output

We look at the result of binarization. If parts of the letters disappear - set the Binarization threshold to 20. In extreme cases - 30. An increased Binarization threshold adds boldness to the text. If the book got pictures, you must use the Mixed mode. Untick Auto layer. Tick Picture zone layer. Let's run the output. The program will automatically find pictures. After the output you need to check behind the program. We look through all the pages with pictures. In the same time we looking for spots on pages that can be deleted in Fill Zones section. If the picture zone was found incorrectly, you need to correct it. You need to go to the Layers section. Either drag vertices. Or delete the zone and create your own. You right-click on the picture, hold down Ctrl to make the area rectangular and draw a rectangle. If the zone has a complex shape, you make a polygon. The picture zone can be used on a part of the picture where the text is poorly recognized and text details will disappear during binarization. Split text and images. Tools->Export...->Export. After processing the images, save the project.

[http://forum.ru-board.com/topic.cgi?forum=5&topic=32945](http://forum.ru-board.com/topic.cgi?forum=5&topic=32945)<br/><br/>

Book Restorer - program for straightening crooked images. Create Book. Tools->Restore. Geometrical correction. Publish (icon of disk in menu). If straightening bitonal image in column Types of files choose G4-compressed, in column Color range - Binary. If straightening text of the book with pictures, you need to input into the program colored images you got from Scan Tailor. TIFF LZW compressed, Color range - RGB colors. Split the straightened images into text and images in Scan Tailor. To avoid crashing from operating heavy amount of images, you should go to Preferences and set JPEG 10% for temporary images.

[http://djvu-converter.narod.ru/](http://djvu-converter.narod.ru/)<br/><br/>

Tsushima - program for clearing slur. Drag images to program icon. Result - images in 8BPP 96DPI format. Convert images to 1BPP 600DPI format in Irfan View.

[http://publ.lib.ru/cgi/forum/YaBB.pl?num=1530528723/13#13](http://publ.lib.ru/cgi/forum/YaBB.pl?num=1530528723/13#13)<br/><br/>

DjVu Small Mod 0.7.6.1 - program for encoding and decoding djvu documents, in other words, for creating djvu documents out of images and extracting images out of djvu documents. For bitonal images use following encoding profile:

Profile set: Original

Type: Bitonal

DPI: 600

[https://book-scan.wixsite.com/djvu/blank-z8lfg](https://book-scan.wixsite.com/djvu/blank-z8lfg)<br/><br/>

DjVu Imager - program for inserting pictures. Set path to djvu document with pictures cutted-out and path of output document. Set the path to out/export/pic folder. Convert. Insert in DjVu. Now you got djvu document with pictures. Settings: BSF - 2, DPI - 300.

[http://www.djvu-soft.narod.ru/scan/djvu_imager_en.htm](http://www.djvu-soft.narod.ru/scan/djvu_imager_en.htm)<br/><br/>

FSD - alternative to Djvu Small Mod + DjVu Imager.

[http://www.djvu-soft.narod.ru/](http://djvu-converter.narod.ru/)

[https://www.youtube.com/watch?v=jOQBTV-zvts](http://djvu-converter.narod.ru/)<br/><br/>

Djvu Small Mod + DjVu Imager and FSD realise method of separated scans. The images are separated into text and pictures, that encoded separately.<br/><br/>

Document Express Editor 6.0.1 - program for deleting/adding images into djvu document. Used for adding a cover. If a line appear in expanded window, use compatibility settings as described for WinDjView.

[http://www.djvu-soft.narod.ru/soft/](http://www.djvu-soft.narod.ru/soft/)<br/><br/>

ABBYY Finereader PDF 15 - program for adding OCR layer. You can use the program to extract tif files from pdf-document. Options->Images processing, set off Split facing pages and Correct page orientation, so OCR layer lies in place. Thorough recognition is necessary. You need only text layer out of output document, so to quicken output, you can set djvu export settings with maximum compression.

[https://rutracker.org/forum/viewtopic.php?t=6040898](https://rutracker.org/forum/viewtopic.php?t=6040898)<br/><br/>

FR11 DjVu Text Layer Crutch - program for fixing OCR layer in FR15 output djvu document and transferring it in initial djvu document (in FR15 output djvu document coloured/grey pictures lose quality).

[https://forum.ru-board.com/topic.cgi?forum=5&topic=38467](https://forum.ru-board.com/topic.cgi?forum=5&topic=38467)<br/><br/>

DjVu Clean Page Inserter - program for inserting empty pages into djvu document.

[https://forum.ru-board.com/topic.cgi?forum=5&topic=38467](https://forum.ru-board.com/topic.cgi?forum=5&topic=38467)<br/><br/>

Pdf & DjVu Bookmarker - program for adding contents. Copy text of contents. Insert in the program. Edit. You can arrange Bookmarks in a hierarchy. Insert into djvu document. Pay your attention to F2 и F3 keys, they quicken work considerably.

[https://sourceforge.net/projects/djvubookmarker/](https://sourceforge.net/projects/djvubookmarker/)<br/><br/>

DjVu Hyperlinks Editor - program for automatic creation of hyperlinks. OCR layer is required. As Shift set difference between number of document page and number of book page. Then set pages of contents / alphabetic index. Choose Job type Content / Alphabetic index 2. Now you got 'hyperlinks, apparent with pointing of cursor on elements of contents' / 'hyperlinks in alphabetic index'.

[http://www.djvu-soft.narod.ru/soft/](http://www.djvu-soft.narod.ru/soft/)<br/><br/>

DjVu Annotations Editor - program for changing properties of hyperlinks. Go to Свойства гиперссылок. Choose Отображать постоянно (if you're changing hyperlinks of alphabetic index), set off Заливка и delete Комментарий. Применить. Сохранить. Open djvu document in Document Express Editor 6.0.1 program and delete hyperlinks on page numbers - Annotation->Delete. To delete/add hyperlinks of contents by hands you need to click Select Annotations in menu - hyperlinks of contents will become apparent. Then, for example, you can edit hyperlink borders, which overlapped several elements of contents and create absent hyperlink by clicking Rectangular Hyperlink in menu and selecting element of contents. In option Style choose Plain Border, Persistent, in option Link - Page Number, in option Page – page of document.

[https://forum.ru-board.com/topic.cgi?forum=5&topic=38467](https://forum.ru-board.com/topic.cgi?forum=5&topic=38467)<br/><br/>

DjVu Chunk Remover - program for deleting chunks, pages in djvu document.

[https://forum.ru-board.com/topic.cgi?forum=5&topic=38467](https://forum.ru-board.com/topic.cgi?forum=5&topic=38467)<br/><br/>

General algorithm:

1) Scan Tailor Universal - images processing.

2) Book Restorer - straightening text lines.

3) Tsushima - cleaning slur.

4) DjVu Small Mod 0.7.6.1 - creation of djvu document.

5) DjVu Imager - inserting coloured/grey pictures.

6) ABBYY Finereader PDF 15 - creation of OCR layer.

7) FR11 DjVu Text Layer Crutch - fixing and transferring OCR layer.

8) Document Express Editor 6.0.1 - adding a cover.

9) Pdf & DjVu Bookmarker - adding a contents.

10) DjVu Hyperlinks Editor - adding hyperlinks.

11) DjVu Annotations Editor - editing style of hyperlinks.

12) Document Express Editor 6.0.1 - editing hyperlinks.<br/><br/>

Publish your book:

Library Genesis - [https://library.bz/main/upload/](https://library.bz/main/upload/)

genesis

upload

RuTracker - [http://rutracker.org/forum/index.php](http://rutracker.org/forum/index.php)<br/><br/>

Information:

[http://www.djvu-soft.narod.ru/](http://www.djvu-soft.narod.ru/)

[http://publ.lib.ru/cgi/forum/YaBB.pl](http://publ.lib.ru/cgi/forum/YaBB.pl)