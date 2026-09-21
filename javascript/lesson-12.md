# JavaScript · Урок 12. DOM: поиск и изменение элементов

## Цели урока
- Находить элементы на странице
- Менять текст, атрибуты, стили; создавать и удалять элементы

## Что такое DOM
Браузер превращает HTML в дерево объектов (Document Object Model). JavaScript может читать и менять это дерево.

## Поиск элементов
```html
<h1 id="title">Заголовок</h1>
<ul class="list"><li>1</li><li>2</li></ul>
```
```js
document.getElementById("title");
document.querySelector(".list");        // первый подходящий
document.querySelectorAll(".list li");  // все подходящие (NodeList)
```

## Изменение содержимого
```js
const title = document.querySelector("#title");
title.textContent = "Новый заголовок";   // безопасный текст
title.innerHTML = "<em>Курсив</em>";     // HTML (осторожно с данными пользователя!)
title.setAttribute("data-id", "5");
title.id;
```

## Стили и классы
```js
title.style.color = "tomato";
title.classList.add("active");
title.classList.remove("active");
title.classList.toggle("hidden");
title.classList.contains("active");
```

## Создание и удаление
```js
const li = document.createElement("li");
li.textContent = "Новый пункт";
document.querySelector(".list").append(li);
li.remove();
```

## Перебор найденных элементов
```js
document.querySelectorAll("li").forEach(item => {
  item.style.fontWeight = "bold";
});
```

## Типичные ошибки
- Скрипт подключён в `<head>` до появления элементов → `null`. Ставьте `<script>` в конец `<body>` или используйте `defer`
- `innerHTML` с данными пользователя — риск XSS; используйте `textContent`
- Ожидают массив от `querySelectorAll` — это `NodeList`

## Практика
1. Измените цвет и текст заголовка со страницы.
2. Добавьте в список 5 пунктов циклом.
3. Сделайте кнопку «Тема», переключающую класс `dark` у `<body>`.

## Проверь себя
1. Чем `textContent` отличается от `innerHTML`?
2. Как найти все элементы с классом?
3. Как создать и добавить элемент?

---
[← Урок 11](lesson-11.md) · [Программа курса](README.md) · [Урок 13 →](lesson-13.md)
