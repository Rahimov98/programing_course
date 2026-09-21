# Python · Урок 6. Циклы: for и while

## Цели урока
- Повторять действия с помощью `for` и `while`
- Управлять циклом через `break`, `continue`

## for и range
```python
for i in range(5):          # 0, 1, 2, 3, 4
    print(i)

for i in range(1, 11, 2):   # 1, 3, 5, 7, 9
    print(i)

for ch in "Python":         # перебор строки
    print(ch)
```

## while
```python
n = 5
while n > 0:
    print(n)
    n -= 1
print("Пуск!")
```

**Бесконечный цикл с выходом**
```python
while True:
    text = input("Введите 'выход': ")
    if text == "выход":
        break
```

## break, continue, else
```python
for i in range(1, 10):
    if i % 2 == 0:
        continue      # пропустить чётные
    if i > 7:
        break         # прервать цикл
    print(i)
else:
    print("Цикл завершён без break")
```

## Вложенные циклы: таблица умножения
```python
for i in range(1, 4):
    for j in range(1, 4):
        print(i * j, end="\t")
    print()
```

## Типичные ошибки
- Забыли изменять переменную в `while` → бесконечный цикл (остановка: `Ctrl+C`)
- `range(5)` не включает 5
- Изменение списка во время итерации по нему

## Практика
1. Выведите сумму чисел от 1 до 100.
2. Напечатайте таблицу умножения на 7.
3. Игра «Угадай число»: компьютер загадывает число 1–20 (`import random`), пользователь угадывает.

## Проверь себя
1. Что выведет `list(range(2, 8, 3))`?
2. Чем `break` отличается от `continue`?
3. Когда выполняется блок `else` у цикла?

---
[← Урок 5](lesson-05.md) · [Программа курса](README.md) · [Урок 7 →](lesson-07.md)
