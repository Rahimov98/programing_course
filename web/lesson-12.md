# Веб · Урок 12. Grid

## Цели урока
- Создавать двумерные сетки
- Размещать элементы по линиям и областям
- Сочетать Grid и Flexbox

## Теория

**Базовая сетка**
```css
.grid {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;   /* 3 равные колонки */
  grid-template-rows: auto;
  gap: 1rem;
}
```

**Повторение и minmax**
```css
grid-template-columns: repeat(3, 1fr);
grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
/* карточки сами подстраиваются под ширину */
```

**Размещение элемента**
```css
.item {
  grid-column: 1 / 3;   /* с линии 1 до 3 */
  grid-row: 2 / 4;
  /* или */
  grid-area: 2 / 1 / 4 / 3;  /* row-start / col-start / row-end / col-end */
}
```

**Именованные области**
```css
.page {
  display: grid;
  grid-template-areas:
    "header header"
    "sidebar main"
    "footer footer";
  grid-template-columns: 200px 1fr;
}
.header  { grid-area: header; }
.sidebar { grid-area: sidebar; }
.main    { grid-area: main; }
.footer  { grid-area: footer; }
```

**Выравнивание**
```css
justify-items: center;   /* ячейки по горизонтали */
align-items: center;     /* по вертикали */
justify-content: center; /* вся сетка */
```

**Grid vs Flexbox**
- Flex — одномерный (ряд или колонка)
- Grid — двумерный (и строки, и колонки)
Часто: Grid для макета страницы, Flex для компонентов внутри.

## Типичные ошибки
- Забыли `display: grid`
- Линии считаются с 1, не с 0
- Слишком сложные области без нужды

## Практика
1. Сетка 3 колонки с `gap`.
2. Адаптивные карточки через `auto-fit` + `minmax`.
3. Макет: header, sidebar, main, footer через `grid-template-areas`.

## Проверь себя
1. Чем Grid отличается от Flexbox?
2. Что делает `minmax(250px, 1fr)`?
3. Как растянуть элемент на две колонки?

---
[← Урок 11](lesson-11.md) · [Программа курса](README.md) · [Урок 13 →](lesson-13.md)
