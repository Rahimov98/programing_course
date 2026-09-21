# JavaScript · Урок 24. Итоговый проект: To-Do приложение

## Цель
Собрать полноценное веб-приложение: HTML + CSS + JavaScript с сохранением данных в `localStorage`.

## Требования
- Добавление, отметка выполненной, удаление задач
- Фильтры: все / активные / выполненные
- Счётчик оставшихся задач
- Сохранение между перезагрузками
- Защита от пустого ввода и XSS

## index.html
```html
<!DOCTYPE html>
<html lang="ru">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>To-Do</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <main class="app">
    <h1>Список дел</h1>
    <form id="form">
      <input id="input" placeholder="Что нужно сделать?" autocomplete="off">
      <button>Добавить</button>
    </form>
    <div class="filters">
      <button data-filter="all" class="active">Все</button>
      <button data-filter="active">Активные</button>
      <button data-filter="done">Выполненные</button>
    </div>
    <ul id="list"></ul>
    <p id="counter"></p>
  </main>
  <script src="app.js"></script>
</body>
</html>
```

## style.css
```css
* { box-sizing: border-box; }
body { font-family: system-ui, sans-serif; background: #f3f4f6; margin: 0; }
.app { max-width: 480px; margin: 40px auto; background: #fff; padding: 24px; border-radius: 12px; }
form { display: flex; gap: 8px; }
input { flex: 1; padding: 10px; border: 1px solid #ccc; border-radius: 8px; }
button { padding: 10px 14px; border: 0; border-radius: 8px; cursor: pointer; }
.filters { margin: 12px 0; display: flex; gap: 6px; }
.filters .active { background: #2563eb; color: #fff; }
ul { list-style: none; padding: 0; }
li { display: flex; justify-content: space-between; padding: 10px 0; border-bottom: 1px solid #eee; }
li.done span { text-decoration: line-through; color: #888; }
```

## app.js
```js
const form = document.querySelector("#form");
const input = document.querySelector("#input");
const list = document.querySelector("#list");
const counter = document.querySelector("#counter");

let tasks = JSON.parse(localStorage.getItem("tasks")) ?? [];
let filter = "all";

const save = () => localStorage.setItem("tasks", JSON.stringify(tasks));

function render() {
  list.innerHTML = "";
  const visible = tasks.filter((t) =>
    filter === "all" ? true : filter === "done" ? t.done : !t.done
  );
  visible.forEach((t) => {
    const li = document.createElement("li");
    li.dataset.id = t.id;
    li.classList.toggle("done", t.done);
    const span = document.createElement("span");
    span.textContent = t.title;
    const del = document.createElement("button");
    del.textContent = "✕";
    del.dataset.action = "delete";
    li.append(span, del);
    list.append(li);
  });
  counter.textContent = `Осталось: ${tasks.filter((t) => !t.done).length}`;
}

form.addEventListener("submit", (e) => {
  e.preventDefault();
  const title = input.value.trim();
  if (!title) return;
  tasks.push({ id: Date.now(), title, done: false });
  input.value = "";
  save();
  render();
});

list.addEventListener("click", (e) => {
  const li = e.target.closest("li");
  if (!li) return;
  const id = Number(li.dataset.id);
  if (e.target.dataset.action === "delete") {
    tasks = tasks.filter((t) => t.id !== id);
  } else {
    const task = tasks.find((t) => t.id === id);
    task.done = !task.done;
  }
  save();
  render();
});

document.querySelector(".filters").addEventListener("click", (e) => {
  if (!e.target.dataset.filter) return;
  filter = e.target.dataset.filter;
  document.querySelectorAll(".filters button").forEach((b) =>
    b.classList.toggle("active", b === e.target)
  );
  render();
});

render();
```

## Задания на усложнение
1. Редактирование задачи по двойному клику.
2. Кнопка «Очистить выполненные».
3. Приоритеты и сроки.
4. Синхронизация с API из урока 23.
5. Загрузите на **GitHub Pages** (см. курс «Веб», урок 17).

## Поздравляем!
Вы прошли курс JavaScript. Следующие шаги: TypeScript, React/Vue, Node.js + база данных, тестирование.

---
[← Урок 23](lesson-23.md) · [Программа курса](README.md)
