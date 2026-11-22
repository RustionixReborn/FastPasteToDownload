# FastPasteToDownload

# Картинка → PNG (PasteToPNG)

Простая программа с оконным интерфейсом: копируешь изображение в буфер обмена, вставляешь в окно — и она сохраняет его как **PNG** в папку `Pictures` рядом с собой.

Написана на Python + Tkinter, для картинок используется Pillow.

## Возможности

- Вставка по **Ctrl+V**, клику по зоне или кнопке.
- Понимает и само изображение в буфере (скриншот, «Копировать изображение»), и скопированные файлы-картинки.
- Автоматически создаёт папку `Pictures` рядом с программой и кладёт туда PNG.
- Уникальные имена по времени (`img_2026-11-22_12-10-20.png`), превью и счётчик сохранений.
- Кнопка «Открыть папку Pictures».

## Запуск

### Готовый .exe (Windows)
Двойной клик по `dist/PasteToPNG.exe` — Python не нужен, всё вшито.

### Из исходника
```bash
pip install Pillow
python paste_to_png.py
```

## Сборка .exe

```bash
pip install pyinstaller Pillow
pyinstaller --onefile --noconsole --name PasteToPNG \
  --exclude-module numpy --exclude-module scipy --exclude-module pandas \
  --exclude-module matplotlib --exclude-module PyQt5 --exclude-module PyQt6 \
  --exclude-module PySide2 --exclude-module PySide6 \
  paste_to_png.py
```

Результат — `dist/PasteToPNG.exe`. Исключения (`--exclude-module`) убирают тяжёлые библиотеки Anaconda, которые программе не нужны: без них сборка ~16 МБ вместо ~168 МБ.

## Как это работает

1. При старте создаётся папка `Pictures` рядом с программой (или с `.exe`).
2. По вставке читается буфер обмена (`PIL.ImageGrab.grabclipboard`).
3. Изображение приводится к совместимому с PNG режиму и сохраняется с уникальным именем.

## Структура

```
paste_to_png.py     # исходный код
README.md
dist/PasteToPNG.exe # собранная программа (генерируется)
Pictures/           # создаётся автоматически при запуске
```

## Требования

- Python 3.10+ (проверено на 3.14) и Pillow — для запуска из исходника.
- Для `.exe` ничего устанавливать не нужно.
