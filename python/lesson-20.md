# Python · Урок 20. Дата и время

## Цели урока
- Работать с датами через `datetime`
- Форматировать и вычислять интервалы

## Основы
```python
from datetime import datetime, date, timedelta

now = datetime.now()
today = date.today()
print(now.year, now.month, now.day, now.hour)

birthday = date(2000, 5, 17)
```

## Форматирование
```python
now.strftime("%d.%m.%Y %H:%M")   # 21.09.2026 14:30
```
Коды: `%d` день, `%m` месяц, `%Y` год, `%H` часы, `%M` минуты, `%S` секунды, `%A` день недели.

## Разбор строки
```python
d = datetime.strptime("15.03.2026", "%d.%m.%Y")
```

## Арифметика
```python
tomorrow = today + timedelta(days=1)
delta = date(2026, 12, 31) - today
print(delta.days)                      # сколько дней до конца года

age = (today - birthday).days // 365
```

## Сравнение
```python
if date(2026, 1, 1) < today:
    print("Уже после 1 января")
```

## Часовые пояса
```python
from zoneinfo import ZoneInfo
dushanbe = datetime.now(ZoneInfo("Asia/Dushanbe"))
```

## Типичные ошибки
- Путаница `%m` (месяц) и `%M` (минуты)
- Вычитание «наивной» и «осведомлённой» о поясах даты — `TypeError`
- Хранение даты как строки вместо объекта

## Практика
1. Выведите, сколько дней осталось до вашего дня рождения.
2. Определите день недели для введённой даты.
3. Напишите функцию, возвращающую возраст в годах.

## Проверь себя
1. Чем `date` отличается от `datetime`?
2. Что делает `strptime`?
3. Что возвращает вычитание двух дат?

---
[← Урок 19](lesson-19.md) · [Программа курса](README.md) · [Урок 21 →](lesson-21.md)
