# Веб · Урок 20. SEO и доступность

## Цели урока
- Делать страницы понятными для поисковиков
- Учитывать доступность (a11y)
- Использовать базовые практики

## Теория

**SEO (минимум)**
```html
<title>Понятный заголовок — до 60 символов</title>
<meta name="description" content="Краткое описание страницы до ~160 символов">
<link rel="canonical" href="https://example.com/page">
```
- Один `<h1>`, логичная иерархия h2–h3
- Осмысленные `alt` у изображений
- Семантические теги
- Нормальная скорость и мобильная вёрстка
- `lang` у html

**Open Graph (для соцсетей)**
```html
<meta property="og:title" content="Заголовок">
<meta property="og:description" content="Описание">
<meta property="og:image" content="https://example.com/preview.jpg">
```

**Доступность**
- Контраст текста и фона (примерно 4.5:1 для обычного текста)
- Фокус с клавиатуры виден
- `label` связан с полями форм
- Кнопки — `<button>`, ссылки — `<a href>`
- Не передавать смысл только цветом

```html
<img src="chart.png" alt="Рост продаж на 20% за квартал">
<button type="button" aria-label="Закрыть">×</button>
```

**ARIA (когда семантики не хватает)**
```html
<nav aria-label="Основное меню">
<div role="dialog" aria-modal="true" aria-labelledby="dlg-title">
```

**Проверка**
- Lighthouse (Chrome DevTools)
- axe / WAVE
- Навигация только с клавиатуры (Tab, Enter, Esc)

## Типичные ошибки
- Пустой или «image1» в alt
- `div` с onclick вместо button/a
- Убрали outline и не дали замену
- Дубли title на всех страницах

## Практика
1. Пропишите title, description и один h1 на своей странице.
2. Проверьте контраст и фокус с клавиатуры.
3. Запустите Lighthouse и исправьте 2–3 замечания.

## Проверь себя
1. Зачем meta description?
2. Что такое достаточный контраст?
3. Чем button отличается от div с кликом для a11y?

---
[← Урок 19](lesson-19.md) · [Программа курса](README.md) · [Урок 21 →](lesson-21.md)
