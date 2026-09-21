# Python · Урок 12. Работа с файлами

## Цели урока
- Читать и записывать текстовые файлы
- Использовать `with` для безопасной работы

## Открытие файла
Режимы: `"r"` — чтение, `"w"` — запись (перезаписывает), `"a"` — добавление, `"r+"` — чтение и запись.

```python
with open("notes.txt", "w", encoding="utf-8") as f:
    f.write("Первая строка\n")
    f.write("Вторая строка\n")
```
`with` автоматически закрывает файл, даже если возникла ошибка.

## Чтение
```python
with open("notes.txt", "r", encoding="utf-8") as f:
    text = f.read()          # весь файл одной строкой

with open("notes.txt", encoding="utf-8") as f:
    for line in f:           # построчно
        print(line.strip())

with open("notes.txt", encoding="utf-8") as f:
    lines = f.readlines()    # список строк
```

## Добавление
```python
with open("notes.txt", "a", encoding="utf-8") as f:
    f.write("Ещё одна строка\n")
```

## Проверка существования
```python
import os
if os.path.exists("notes.txt"):
    print("Файл найден")
```
Современный вариант — `pathlib`:
```python
from pathlib import Path
p = Path("notes.txt")
print(p.exists(), p.read_text(encoding="utf-8"))
```

## Типичные ошибки
- Не указали `encoding="utf-8"` — проблемы с кириллицей на Windows
- Режим `"w"` стирает содержимое файла
- `FileNotFoundError` — неверный путь или рабочая папка

## Практика
1. Запишите в файл 5 введённых пользователем строк.
2. Посчитайте число строк и слов в файле.
3. Сделайте «дневник»: каждая запись добавляется с датой.

## Проверь себя
1. Зачем нужен `with`?
2. Чем `"w"` отличается от `"a"`?
3. Как прочитать файл построчно?

---
[← Урок 11](lesson-11.md) · [Программа курса](README.md) · [Урок 13 →](lesson-13.md)
