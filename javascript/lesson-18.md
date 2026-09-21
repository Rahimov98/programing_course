# JavaScript · Урок 18. Промисы

## Цели урока
- Понимать асинхронность и колбэки
- Работать с `Promise`, `then`, `catch`

## Асинхронность
JavaScript однопоточный, но долгие операции (таймеры, сеть) выполняются «в фоне», а результат приходит позже.
```js
console.log(1);
setTimeout(() => console.log(2), 1000);
console.log(3);
// 1, 3, затем 2
```

## Промис
Объект, представляющий результат, который будет получен позже. Состояния: **pending** → **fulfilled** или **rejected**.
```js
const wait = (ms) => new Promise((resolve) => setTimeout(resolve, ms));

const check = (n) =>
  new Promise((resolve, reject) => {
    if (n > 0) resolve("Положительное");
    else reject(new Error("Не положительное"));
  });

check(5)
  .then((msg) => console.log(msg))
  .catch((err) => console.log(err.message))
  .finally(() => console.log("Готово"));
```

## Цепочки
```js
wait(500)
  .then(() => { console.log("0.5 с"); return wait(500); })
  .then(() => console.log("1 с"));
```

## Комбинаторы
```js
Promise.all([p1, p2, p3]);        // ждать все; ошибка любого — ошибка всех
Promise.allSettled([p1, p2]);     // результаты всех, даже с ошибками
Promise.race([p1, p2]);           // первый завершившийся
Promise.any([p1, p2]);            // первый успешный
```

## Порядок выполнения
Микрозадачи (`then`) выполняются раньше макрозадач (`setTimeout`):
```js
setTimeout(() => console.log("timeout"), 0);
Promise.resolve().then(() => console.log("promise"));
// promise, timeout
```

## Типичные ошибки
- Забыли `return` в цепочке `then`
- Нет `catch` — ошибки теряются
- Создают промисы там, где они не нужны

## Практика
1. Функция `delay(ms)`, возвращающая промис-таймер.
2. Выведите 3 сообщения с паузой в секунду через цепочку.
3. Запустите 3 таймера параллельно и дождитесь всех через `Promise.all`.

## Проверь себя
1. Какие состояния у промиса?
2. Чем `Promise.all` отличается от `Promise.allSettled`?
3. Что выведет код с `setTimeout(..., 0)` и `Promise.resolve().then(...)`?

---
[← Урок 17](lesson-17.md) · [Программа курса](README.md) · [Урок 19 →](lesson-19.md)
