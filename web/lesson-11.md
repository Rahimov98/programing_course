# Веб · Урок 11. Flexbox

## Цели урока
- Выстраивать элементы в ряд или колонку
- Выравнивать по главной и поперечной оси
- Делать гибкие карточки и меню

## Теория

**Контейнер**
```css
.container {
  display: flex;
  flex-direction: row;      /* row | column | row-reverse | column-reverse */
  justify-content: center;  /* главная ось: start | end | center | space-between | space-around */
  align-items: center;      /* поперечная ось */
  flex-wrap: wrap;          /* перенос */
  gap: 16px;                /* промежутки */
}
```

**Элементы**
```css
.item {
  flex-grow: 1;     /* может расти */
  flex-shrink: 1;   /* может сжиматься */
  flex-basis: 200px; /* базовый размер */
  /* сокращение: flex: 1 1 200px; */
  align-self: flex-end;  /* своё выравнивание */
}
```

**Типичные паттерны**
```css
/* Горизонтальное меню */
nav {
  display: flex;
  gap: 1rem;
  justify-content: flex-end;
}

/* Карточки в ряд с переносом */
.cards {
  display: flex;
  flex-wrap: wrap;
  gap: 1rem;
}
.card {
  flex: 1 1 250px;  /* минимум ~250px, растягиваются */
}

/* Центр по вертикали и горизонтали */
.hero {
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 60vh;
}
```

## Типичные ошибки
- Забыли `display: flex` на родителе
- Путаница main axis / cross axis при `flex-direction: column`
- `gap` не работает в очень старых браузерах (сейчас почти везде ок)

## Практика
1. Горизонтальное меню с `space-between` или `gap`.
2. Три карточки в ряд, на узком экране — друг под другом (`flex-wrap`).
3. Отцентрируйте блок по центру экрана через flex.

## Проверь себя
1. Чем `justify-content` отличается от `align-items`?
2. Что делает `flex: 1`?
3. Зачем `flex-wrap`?

---
[← Урок 10](lesson-10.md) · [Программа курса](README.md) · [Урок 12 →](lesson-12.md)
