# Веб · Урок 13. Адаптивность и media queries

## Цели урока
- Делать сайты удобными на телефоне и десктопе
- Писать media queries
- Использовать относительные единицы и гибкие сетки

## Теория

**Viewport (уже в head)**
```html
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```

**Media queries**
```css
/* Мобильный сначала (mobile-first) */
.container {
  padding: 1rem;
}

@media (min-width: 768px) {
  .container {
    padding: 2rem;
    max-width: 720px;
    margin: 0 auto;
  }
}

@media (min-width: 1024px) {
  .container {
    max-width: 960px;
  }
  .cards {
    grid-template-columns: repeat(3, 1fr);
  }
}
```

**Полезные условия**
```css
@media (max-width: 600px) { }
@media (orientation: landscape) { }
@media (prefers-color-scheme: dark) {
  body { background: #111; color: #eee; }
}
```

**Гибкие изображения**
```css
img {
  max-width: 100%;
  height: auto;
  display: block;
}
```

**Типичные брейкпоинты**
- ~480px — большие телефоны
- ~768px — планшеты
- ~1024px — ноутбуки
- ~1280px — десктоп

**Подход**
1. Верстайте сначала под мобильный
2. Добавляйте сложности на больших экранах (`min-width`)
3. Проверяйте в DevTools (режим устройства)

## Типичные ошибки
- Забыли viewport
- Фиксированные ширины в px везде
- Только `max-width` без mobile-first

## Практика
1. Сделайте контейнер с разным padding на мобильном и десктопе.
2. Карточки: 1 колонка на телефоне, 3 на десктопе.
3. Скройте боковое меню на узких экранах (`display: none`).

## Проверь себя
1. Что такое mobile-first?
2. Зачем meta viewport?
3. Как сделать картинку адаптивной?

---
[← Урок 12](lesson-12.md) · [Программа курса](README.md) · [Урок 14 →](lesson-14.md)
