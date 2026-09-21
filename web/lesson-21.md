# Веб · Урок 21. Производительность и оптимизация

## Цели урока
- Ускорять загрузку страницы
- Оптимизировать изображения и CSS/JS
- Измерять результат

## Теория

**Что влияет на скорость**
- Размер и количество файлов
- Изображения
- Блокирующие скрипты/стили
- Шрифты
- Лишний JavaScript

**Изображения**
```html
<img src="photo.jpg" alt="..." width="800" height="600" loading="lazy">
```
- Сжимайте (Squoosh, ImageOptim)
- Современные форматы: WebP, AVIF
- Указывайте width/height — меньше сдвига вёрстки (CLS)
- `loading="lazy"` для картинок ниже сгиба

**CSS и JS**
```html
<link rel="stylesheet" href="styles.css">
<script src="app.js" defer></script>
```
- Минификация на проде
- Не подключать огромные библиотеки ради мелочи
- Критический CSS — по возможности

**Шрифты**
```css
font-display: swap;  /* текст виден сразу запасным шрифтом */
```
```html
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
```

**Метрики (Core Web Vitals)**
- LCP — скорость отрисовки основного контента
- INP / FID — отзывчивость
- CLS — стабильность вёрстки

**Инструменты**
- Chrome Lighthouse
- Network и Performance в DevTools
- PageSpeed Insights

## Типичные ошибки
- Картинки по 5 МБ «как есть»
- Десять скриптов в head без defer
- Шрифты без font-display

## Практика
1. Сожмите изображения и добавьте loading="lazy".
2. Перенесите script в конец или поставьте defer.
3. Прогоните Lighthouse и сравните Performance до/после.

## Проверь себя
1. Зачем width и height у img?
2. Что даёт loading="lazy"?
3. Назовите одну метрику Core Web Vitals.

---
[← Урок 20](lesson-20.md) · [Программа курса](README.md) · [Урок 22 →](lesson-22.md)
