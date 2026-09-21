# JavaScript · Урок 19. async/await и fetch

## Цели урока
- Писать асинхронный код линейно
- Получать данные с сервера через `fetch`

## async / await
```js
const wait = (ms) => new Promise((r) => setTimeout(r, ms));

async function run() {
  console.log("Начали");
  await wait(1000);          // «пауза» без блокировки страницы
  console.log("Через секунду");
}
run();
```
`async`-функция всегда возвращает промис. `await` работает только внутри `async` (и на верхнем уровне модулей).

## fetch
```js
async function loadUser() {
  try {
    const response = await fetch("https://jsonplaceholder.typicode.com/users/1");
    if (!response.ok) throw new Error(`HTTP ${response.status}`);
    const user = await response.json();
    console.log(user.name, user.email);
  } catch (err) {
    console.log("Ошибка загрузки:", err.message);
  }
}
loadUser();
```
`fetch` отклоняется только при сетевой ошибке; коды 404/500 нужно проверять через `response.ok`.

## POST-запрос
```js
const res = await fetch("https://jsonplaceholder.typicode.com/posts", {
  method: "POST",
  headers: { "Content-Type": "application/json" },
  body: JSON.stringify({ title: "Привет", body: "Текст", userId: 1 }),
});
console.log(await res.json());
```

## Параллельные запросы
```js
const [users, posts] = await Promise.all([
  fetch(url1).then((r) => r.json()),
  fetch(url2).then((r) => r.json()),
]);
```

## Индикатор загрузки
```js
loader.hidden = false;
try { /* запрос */ } finally { loader.hidden = true; }
```

## Типичные ошибки
- Забыли `await` — получили промис вместо данных
- Не проверили `response.ok`
- Последовательные `await` там, где запросы можно выполнить параллельно
- CORS: сервер должен разрешать запросы с вашего домена

## Практика
1. Загрузите список пользователей и выведите имена в `<ul>`.
2. Покажите «Загрузка...» на время запроса и сообщение при ошибке.
3. Сделайте поиск: по вводу id показывать пост.

## Проверь себя
1. Что возвращает `async`-функция?
2. Отклоняется ли `fetch` при ответе 404?
3. Как выполнить два запроса параллельно?

---
[← Урок 18](lesson-18.md) · [Программа курса](README.md) · [Урок 20 →](lesson-20.md)
