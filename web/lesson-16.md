# Веб · Урок 16. CSS-переменные и организация кода

## Цели урока
- Объявлять и использовать CSS-переменные
- Организовать стили по файлам/секциям
- Поддерживать тему (светлая/тёмная)

## Теория

**CSS-переменные (custom properties)**
```css
:root {
  --color-primary: #3366ff;
  --color-text: #1a1a1a;
  --color-bg: #ffffff;
  --space-m: 1rem;
  --radius: 8px;
  --font-main: "Inter", system-ui, sans-serif;
}

body {
  color: var(--color-text);
  background: var(--color-bg);
  font-family: var(--font-main);
}

.button {
  background: var(--color-primary);
  padding: var(--space-m);
  border-radius: var(--radius);
}
```

**Переопределение**
```css
.card {
  --color-primary: #22aa66;  /* локально для .card и потомков */
}

@media (prefers-color-scheme: dark) {
  :root {
    --color-text: #eee;
    --color-bg: #121212;
  }
}
```

**Fallback**
```css
color: var(--color-text, #333);
```

**Организация**
```
styles/
  reset.css      /* сброс отступов */
  variables.css  /* :root */
  base.css       /* body, typography */
  layout.css     /* сетка, контейнеры */
  components.css /* кнопки, карточки */
  utilities.css  /* мелкие хелперы */
```
Или один файл с комментариями-секциями.

**Методологии (обзор)**
- BEM: `.card`, `.card__title`, `.card--featured`
- Утилитарные классы (как в Tailwind)
- Главное — единый стиль имён в проекте

## Типичные ошибки
- Переменные без `:root` или родителя
- Слишком много «магических» чисел вместо переменных
- Дублирование одних и тех же значений

## Практика
1. Вынесите цвета и отступы в `:root`.
2. Сделайте тёмную тему через `prefers-color-scheme` или класс `.theme-dark`.
3. Разделите стили на логические блоки с комментариями.

## Проверь себя
1. Зачем CSS-переменные?
2. Как задать значение по умолчанию в `var()`?
3. Что такое BEM в двух словах?

---
[← Урок 15](lesson-15.md) · [Программа курса](README.md) · [Урок 17 →](lesson-17.md)
