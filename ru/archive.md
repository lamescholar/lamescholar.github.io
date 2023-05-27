**Internet Archive**<br/><br/>

<https://github.com/MiniGlome/Archive.org-Downloader><br/><br/>

С помощью этого скрипта ты можешь скачать книгу с Internet Archive. Скрипт использует 1 час книговыдачи для загрузки страниц книги. Для преобразования изображений в PDF скрипт использует пакет img2pdf. Но он создает слишком большой PDF-файл. Поэтому я рекомендую тебе сохранить параметр -j в конце команды, чтобы получить только изображения. Ниже указаны три варианта того, как вы можете эффективно конвертировать их в PDF или DjVu.<br/><br/>

Для установки необходимы:

Git - <https://git-scm.com/download/win>

Python - <https://www.python.org/downloads/>

При установке Python нужно поставить галочку Add python.exe to PATH.<br/><br/>

Установка:

```
Win+R
cmd
cd C:\
git clone https://github.com/MiniGlome/Archive.org-Downloader.git
cd Archive.org-Downloader
pip install -r requirements.txt
```
<br/><br/>
Перед использованием необходимо зарегистрироваться.

<https://archive.org/account/signup><br/><br/>

Использование:

```
Win+R
cmd
cd C:\Archive.org-Downloader
python archive-org-downloader.py -e email -p пароль -r 0 -u https://archive.org/details/untoldhistoryoft00ston -j
```
<br/><br/>
Картинки скачиваются без определённого DPI. Из-за этого могут быть проблемы при создании файла. DPI можно установить с помощью программы Irfan View.

Помимо правки DPI, если сканы тёмные, а текст блеклый, в программе Irfan View можно использовать инструменты цветокоррекции Contrast и Gamma correction. Я использую следующую сетку значений (первый столбик - Contrast, второй - Gamma correction):

90 4.00

70 3.00

50 2.00

30 1.50

Это значения для случая, когда скан тёмный и его надо подсветлить. Если стандратные варианты не подходят, нужно экспериментировать с разными комбинациями - Shift+G. Визуально Contrast жирнит текст, повышает яркость фона. Gamma correction подсветляет скан, но выцветляет текст. Полезные комбинации: 70 2.00 (скан не сильно тёмный, есть зеленоватый или оранжевый оттенок), только Contrast - 50/70 (скан не сильно тёмный, текст блеклый), 50 0.75 (скан довольно светлый, текст блеклый), только Gamma correction - 0.62 (скан очень светлый).

Если остался зеленоватый или оранжевый оттенок, можно понизить насыщенность цветов скана. Для этого используется инструмент Saturation. Значение - -100/-150.

Помимо инструментов цветокоррекции, очень часто пригождается инструмент Sharpen. Используется при наличии размытого текста (дефект фотографирования). Оптимальное значение - 30.<br/><br/>

Правка DPI:

IrfanView - <https://www.irfanview.com/>

File->Batch Conversion/Rename...

Добавляешь картинки. Sort files. By Name. Auto sort file list after insert. Add all.

Output format:->JPG

Use advanced options (for bulk resize...)->Advanced->Save new DPI value: 300 или 600. Если ширина картинок меньше 2500 - 300 DPI, больше 2500 - 600 DPI. Вводишь значения Gamma correction, Constrast и Saturation, если необходимо. Sharpen: 30, если необходимо.

Выбираешь выходную папку.

Start Batch.<br/><br/>

Преобразование JPG в PDF:

LuraTech PDF Compressor - <https://archive.org/details/LuraTechPDFCompressorDesktopV6.2.0.4>

Настройки:

Profile: Standart

Quality: 9

или

Profile: Photo

Quality: 6

Программа не распознаёт русский язык.

ABBYY Finereader (текстовый слой) - <https://rutracker.org/forum/viewtopic.php?t=6040898><br/><br/>

или<br/><br/>

Преобразование JPG в PDF:

Adobe Acrobat XI Pro - <https://rutracker.org/forum/viewtopic.php?t=5480244>

Создать->Объединить файлы в один документ PDF...->Параметры->Всегда добавлять закладки в Adobe PDF. Убрать галочку.

Добавить файлы...->Добавить файлы...->Объединить файлы.

Инструменты->Распознавание текста->В этом файле->Изменить...

Выбери подходящий язык распознавания.

PDF на выходе: ClearScan

300 dpi

Файл->Сохранить.<br/><br/>

или<br/><br/>

Преобразование JPG в DjVu:

Обработка JPG-картинок в Scan Tailor.

См. [DjVu](https://lamescholar.github.io/ru/djvu).<br/><br/>

Не забудь удалить папки с картинками.<br/><br/>

Где опубликовать книгу:

Library Genesis - <https://library.bz/main/upload/>

genesis

upload

RuTracker - <http://rutracker.org/forum/index.php>