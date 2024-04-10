---
title: Internet Archive
---

<https://github.com/MiniGlome/Archive.org-Downloader>
<br><br>

С помощью этого скрипта ты можешь скачать любую книгу с Internet Archive. В случае книг, защищенных авторским правом, для загрузки страниц книги cкрипт использует 1 час книговыдачи. Для преобразования изображений в PDF скрипт использует пакет img2pdf. Но он создает большой PDF-файл. Поэтому я рекомендую тебе сохранить параметр -j в конце команды, чтобы получить только изображения. Ниже указаны три варианта того, как ты можешь эффективно конвертировать их в PDF или DjVu.
<br><br>

#### Для установки необходимы:

Git - <https://git-scm.com/download/win>

Python - <https://www.python.org/downloads/>

При установке Python нужно поставить галочку Add python.exe to PATH.
<br><br>

#### Установка:

Win+R cmd

```
cd C:\
git clone https://github.com/MiniGlome/Archive.org-Downloader.git
cd Archive.org-Downloader
pip install -r requirements.txt
```
<br>

Перед использованием необходимо зарегистрироваться:

<https://archive.org/account/signup>

Если у тебя плохое зрение, ты можешь получить доступ ко всем книгам и микрофильмам:

<https://docs.google.com/forms/d/e/1FAIpQLScSBbT17HSQywTm-fQawOK7G4dN-QPbDWNstdfvysoKTXCjKA/viewform>
<br><br>

#### Скачивание картинок:

Win+R cmd

```
cd C:\Archive.org-Downloader
python archive-org-downloader.py -e email -p пароль -r 0 -u https://archive.org/details/untoldhistoryoft00ston -j
```
<br>

На данном этапе можно обработать картинки в Scan Tailor и кодировать их в DjVu-файл с помощью DjVu Small Mod.

См. [DjVu](/ru/djvu).

Или можно произвести цветокоррекцию и кодировать картинки в PDF-файл.
<br><br>

#### Цветокоррекция

Если сканы тёмные, а текст блеклый, можно использовать инструменты цветокоррекции Contrast и Gamma correction в программе IrfanView . Я использую следующую сетку значений (первый столбик - Contrast, второй - Gamma correction):

90 4.00

70 3.00

50 2.00

Это значения для случая, когда скан тёмный и его надо подсветлить. Если стандартные варианты не подходят, нужно экспериментировать с разными комбинациями - Shift+G. Визуально Contrast жирнит текст и повышает яркость фона. Gamma correction подсветляет скан, но выцветляет текст. Полезные комбинации: 70 2.00 (скан не сильно тёмный, есть зеленоватый или оранжевый оттенок), только Contrast - 50/70 (скан не сильно тёмный, текст блеклый), 50 0.75 (скан довольно светлый, текст блеклый), только Gamma correction - 0.62 (скан очень светлый).

Если остался зеленоватый или оранжевый оттенок, можно понизить насыщенность цветов скана. Для этого используется инструмент Saturation. Значение - -100/-150.

Цветокоррекцию к обложке лучше применять отдельно. Часто подходит комбинация 50 2.00, иногда просто 2.00, когда фотография очень тёмная.

Помимо инструментов цветокоррекции, очень часто пригождается инструмент Sharpen. Используется при наличии размытого текста (дефект фотографирования). Оптимальное значение - 30.

Скрипт скачивает картинки без определённого DPI. Из-за этого могут быть проблемы при создании файла. DPI устанавливается в той же программе IrfanView.

IrfanView - <https://www.irfanview.com/>

Открываешь одну из страниц книги.

File->Batch Conversion/Rename...

Добавляешь картинки. Sort files. By Name. Auto sort file list after insert. Add all.

Output format:->JPG

Use advanced options (for bulk resize...)->Advanced->Save new DPI value: 300 или 600. Если ширина картинок меньше 2500 - 300 DPI, больше 2500 - 600 DPI. В случае с LuraTech PDF Compressor 300 DPI устанавливать не обязательно - это значение по умолчанию, когда DPI не установлено. Вводишь значения Gamma correction, Constrast, Saturation, Sharpen, если необходимо.

Выбираешь выходную папку.

Start Batch.
<br><br>

#### Кодирование картинок в PDF-файл:

**Вариант №1:**

LuraTech PDF Compressor - <https://archive.org/details/LuraTechPDFCompressorDesktopV6.2.0.4>

Настройки:

Profile: Standart

Quality: 9

или

Profile: Photo

Quality: 7

или

Profile: B/W

Quality: 10

Программа не распознаёт русский язык.

ABBYY Finereader (текстовый слой) - <https://btdig.com/db98398f6d1c9bbd4c8ac905dc30abb5f9e4b704/abbyy-finereader-kpojiuk>

**Вариант №2:**

Adobe Acrobat XI Pro - <https://rutracker.org/forum/viewtopic.php?t=5480244>

Создать->Объединить файлы в один документ PDF...->Параметры->Всегда добавлять закладки в Adobe PDF. Убрать галочку.

Добавить файлы...->Добавить файлы...->Объединить файлы.

Инструменты->Распознавание текста->В этом файле->Изменить...

Выбери подходящий язык распознавания.

PDF на выходе: ClearScan

300 dpi

Файл->Сохранить.
<br><br>

Не забудь удалить папки с картинками.
<br><br>

#### Где опубликовать книгу:

Library Genesis - <https://library.bz/main/upload/>

genesis

upload

RuTracker - <http://rutracker.org/forum/index.php>

VK - <https://vk.com/docs>