# Веб · Урок 8. Цвета, шрифты, текст

## Цели урока
- Задавать цвета разными способами
- Подключать и настраивать шрифты
- Стилизовать текст

## Теория

**Цвета**
```css
color: red;                    /* имя */
color: #ff0000;                /* hex */
color: #f00;                   /* короткий hex */
color: rgb(255, 0, 0);
color: rgba(255, 0, 0, 0.5);   /* с прозрачностью */
color: hsl(0, 100%, 50%);
background-color: #1a1a2e;
```

**Шрифты**
```css
font-family: "Segoe UI", Arial, sans-serif;
font-size: 16px;        /* или 1rem, 1.2em */
font-weight: 700;       /* 400 — normal, 700 — bold */
font-style: italic;
line-height: 1.5;
```

**Подключение веб-шрифта (Google Fonts)**
```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Roboto:wght@400;700&display=swap" rel="stylesheet">
```
```css
body {
  font-family: "Roboto", sans-serif;
}
```

**Текст**
```css
text-align: center;      /* left | right | justify */
text-decoration: none;   /* у ссылок часто убирают подчёркивание */
text-transform: uppercase;
letter-spacing: 0.05em;
text-shadow: 1px 1px 2px rgba(0,0,0,0.3);
```

**Единицы**
- `px` — пиксели
- `rem` — относительно корня (удобно для масштабирования)
- `em` — относительно родителя
- `%` — относительно родителя

## Типичные ошибки
- Слишком мелкий шрифт на мобильных
- Низкий контраст текста и фона
- Забыли запасной шрифт в `font-family`

## Практика
1. Задайте цвет фона и текста страницы.
2. Подключите Google Font и примените к заголовкам.
3. Стилизуйте абзацы: размер, межстрочный интервал, выравнивание.

## Проверь себя
1. Чем `rem` удобнее `px`?
2. Зачем запасные шрифты в `font-family`?
3. Как задать полупрозрачный цвет?

---
[← Урок 7](lesson-07.md) · [Программа курса](README.md) · [Урок 9 →](lesson-09.md)
