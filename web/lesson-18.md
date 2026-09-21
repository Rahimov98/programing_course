# Веб · Урок 18. Основы JS для веба

## Цели урока
- Подключать JavaScript к странице
- Реагировать на клики и менять DOM
- Делать простые интерактивные элементы

## Теория

**Подключение**
```html
<script src="script.js" defer></script>
<!-- defer — после разбора HTML, порядок сохраняется -->
```

**Выбор элементов**
```js
const btn = document.querySelector(".btn");
const items = document.querySelectorAll(".item");
const title = document.getElementById("title");
```

**События**
```js
btn.addEventListener("click", () => {
  title.textContent = "Нажали!";
  title.classList.toggle("active");
});
```

**Изменение DOM**
```js
el.textContent = "Новый текст";
el.innerHTML = "<strong>Жирный</strong>";  // осторожно с XSS
el.classList.add("hidden");
el.classList.remove("hidden");
el.style.color = "red";  // лучше через классы
```

**Простой пример: переключатель темы**
```js
const toggle = document.querySelector("#theme-toggle");
toggle.addEventListener("click", () => {
  document.body.classList.toggle("theme-dark");
});
```

**Мобильное меню**
```js
const burger = document.querySelector(".burger");
const nav = document.querySelector("nav");
burger.addEventListener("click", () => {
  nav.classList.toggle("open");
});
```

## Типичные ошибки
- Скрипт в `<head>` без defer/DOMContentLoaded → элементов ещё нет
- `innerHTML` с данными пользователя без очистки
- Забыли `addEventListener` и пишут `onclick` в HTML

## Практика
1. Кнопка меняет текст заголовка.
2. Переключатель светлой/тёмной темы (класс на body).
3. Кнопка «бургер» открывает/закрывает меню.

## Проверь себя
1. Зачем `defer` у script?
2. Чем `textContent` безопаснее `innerHTML`?
3. Как добавить/убрать класс у элемента?

---
[← Урок 17](lesson-17.md) · [Программа курса](README.md) · [Урок 19 →](lesson-19.md)
