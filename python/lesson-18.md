# Python · Урок 18. JSON и CSV

## Цели урока
- Сохранять и читать структурированные данные
- Работать с модулями `json` и `csv`

## JSON
Формат обмена данными, похож на словари и списки Python.
```python
import json

data = {"name": "Алишер", "age": 21, "skills": ["Python", "SQL"]}

text = json.dumps(data, ensure_ascii=False, indent=2)   # объект → строка
obj = json.loads(text)                                  # строка → объект

with open("data.json", "w", encoding="utf-8") as f:
    json.dump(data, f, ensure_ascii=False, indent=2)

with open("data.json", encoding="utf-8") as f:
    loaded = json.load(f)
print(loaded["skills"][0])
```
Соответствия: `dict` ↔ object, `list` ↔ array, `str` ↔ string, `None` ↔ null, `True` ↔ true.

## CSV
Табличные данные (Excel, выгрузки).
```python
import csv

rows = [["name", "age"], ["Алишер", 21], ["Мадина", 19]]
with open("people.csv", "w", newline="", encoding="utf-8") as f:
    csv.writer(f).writerows(rows)

with open("people.csv", newline="", encoding="utf-8") as f:
    for row in csv.DictReader(f):
        print(row["name"], row["age"])
```

## Типичные ошибки
- Без `ensure_ascii=False` кириллица превращается в `\u0410...`
- Без `newline=""` в CSV на Windows появляются пустые строки
- Все значения, прочитанные из CSV, — строки; приводите к `int` вручную
- Не все объекты сериализуются в JSON (например, `datetime`, `set`)

## Практика
1. Сохраните список студентов в `students.json` и прочитайте обратно.
2. Прочитайте CSV и найдите средний возраст.
3. Конвертируйте CSV в JSON.

## Проверь себя
1. Чем `dumps` отличается от `dump`?
2. Как читать CSV как словари?
3. Почему нужен `ensure_ascii=False`?

---
[← Урок 17](lesson-17.md) · [Программа курса](README.md) · [Урок 19 →](lesson-19.md)
