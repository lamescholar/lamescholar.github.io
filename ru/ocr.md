**OCR**<br/><br/>

Эти программы позволяют получить текст из скриншота. Для добавления текстового слоя смотри [DjVu](https://lamescholar.github.io/ru/djvu) и [PDF](https://lamescholar.github.io/ru/pdf).<br/><br/>

ABBYY Screenshot Reader - <https://rutracker.org/forum/viewtopic.php?t=6040898><br/><br/>

ABBYY Screenshot Reader не всегда работает как следует. Например, он плохо работает со старыми немецкими шрифтами или какими-либо волнистыми шрифтами. Tesseract справляется с этим лучше.<br/><br/>

Tesseract:

<https://github.com/UB-Mannheim/tesseract/wiki>

<https://tesseract-ocr.github.io/tessdoc/Command-Line-Usage.html>

Установи Tesseract со всеми языковыми дополнения. Добавь установочную папку в PATH.

Теперь, допустим, у тебя лежит скриншот немецкого текста на Рабочем столе - 1.jpg. Или ты можешь сделать вырезку с помощью IrfanView. Ctrl+Y, S.

Использование:

```
Win+R
cmd
cd desktop
tesseract 1.jpg - -l deu
```

Ты получаешь текст прямо в командной строке.<br/><br/>

Capture2Text - <https://capture2text.sourceforge.net/>

Ставишь мышь в угол текста. Win+Q. Выводишь прямоугольник. Текст распознаётся в буфер.

Программа распознаёт Tesseract'ом. Тренировочные файлы устарели - 2015 года. Их необходимо заменить. Удаляешь папку tessdata. Копируешь и вставляешь папку tessdata из установочной папки Tesseract'а.

<https://github.com/UB-Mannheim/tesseract/wiki><br/><br/>

Для перевода пользуй ChatGPT. Смотри [ChatGPT](https://lamescholar.github.io/ru/chatgpt).