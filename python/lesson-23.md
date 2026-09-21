# Python · Урок 23. Tkinter: графический интерфейс

## Цели урока
- Создать окно с элементами управления
- Обрабатывать нажатия кнопок

## Первое окно
```python
import tkinter as tk

root = tk.Tk()
root.title("Моё приложение")
root.geometry("300x200")

label = tk.Label(root, text="Привет!", font=("Arial", 14))
label.pack(pady=10)

root.mainloop()
```

## Виджеты
`Label` — текст, `Button` — кнопка, `Entry` — поле ввода, `Text` — многострочный текст, `Checkbutton`, `Radiobutton`, `Listbox`, `Canvas`.

## Пример: приветствие
```python
import tkinter as tk
from tkinter import messagebox

def greet():
    name = entry.get().strip()
    if not name:
        messagebox.showwarning("Ошибка", "Введите имя")
        return
    label.config(text=f"Привет, {name}!")

root = tk.Tk()
root.title("Приветствие")

entry = tk.Entry(root, width=25)
entry.pack(padx=10, pady=10)

tk.Button(root, text="Поздороваться", command=greet).pack()
label = tk.Label(root, text="")
label.pack(pady=10)

root.mainloop()
```

## Расположение элементов
- `pack()` — вертикально/горизонтально по порядку
- `grid(row=0, column=1)` — сетка
- `place(x=10, y=20)` — точные координаты

## Пример: счётчик
```python
count = 0
def inc():
    global count
    count += 1
    lbl.config(text=str(count))
```

## Типичные ошибки
- `command=greet()` вместо `command=greet` — функция вызовется сразу
- Смешивание `pack` и `grid` в одном контейнере
- Долгие операции внутри обработчика «замораживают» окно

## Практика
1. Калькулятор с двумя полями ввода и кнопкой «Сложить».
2. Приложение-счётчик с кнопками «+» и «−».
3. Список дел с полем ввода и `Listbox`.

## Проверь себя
1. Что делает `mainloop()`?
2. Чем `grid` отличается от `pack`?
3. Почему нельзя писать `command=func()`?

---
[← Урок 22](lesson-22.md) · [Программа курса](README.md) · [Урок 24 →](lesson-24.md)
