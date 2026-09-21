# Python · Урок 14. Модули и pip

## Цели урока
- Подключать стандартные и сторонние модули
- Создавать собственные модули
- Устанавливать пакеты через `pip`

## Импорт
```python
import math
print(math.sqrt(16), math.pi)

from random import randint, choice
print(randint(1, 6), choice(["a", "b"]))

import datetime as dt
```
Полезные модули стандартной библиотеки: `math`, `random`, `os`, `sys`, `json`, `datetime`, `collections`, `pathlib`.

## Свой модуль
Файл `tools.py`:
```python
def double(x):
    return x * 2

if __name__ == "__main__":
    print("Запущено напрямую")
```
Использование в `main.py`:
```python
import tools
print(tools.double(21))
```
Блок `if __name__ == "__main__":` выполняется только при прямом запуске файла.

## pip
```bash
pip install requests
pip list
pip uninstall requests
pip freeze > requirements.txt
pip install -r requirements.txt
```

## Виртуальное окружение
Изолирует библиотеки проекта:
```bash
python -m venv venv
venv\Scripts\activate        # Windows
source venv/bin/activate     # Linux/macOS
```

## Типичные ошибки
- Назвали свой файл `random.py` или `math.py` — он перекроет стандартный модуль
- `ModuleNotFoundError` — пакет не установлен в текущем окружении
- Установили пакет в одно окружение, запускаете из другого

## Практика
1. Модуль `geometry.py` с функциями площади круга и прямоугольника.
2. Установите `requests` и получите код ответа `https://example.com`.
3. Создайте виртуальное окружение и `requirements.txt`.

## Проверь себя
1. Зачем `if __name__ == "__main__"`?
2. Что такое виртуальное окружение?
3. Как установить все зависимости из `requirements.txt`?

---
[← Урок 13](lesson-13.md) · [Программа курса](README.md) · [Урок 15 →](lesson-15.md)
