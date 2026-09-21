# JavaScript · Урок 6. Функции

## Цели урока
- Объявлять функции разными способами
- Понимать параметры, возврат значения и параметры по умолчанию

## Function Declaration
```js
function greet(name) {
  return `Привет, ${name}!`;
}
console.log(greet("Мадина"));
```
Такие функции «поднимаются» — их можно вызвать до объявления.

## Function Expression
```js
const square = function (x) {
  return x * x;
};
```

## Параметры по умолчанию и rest
```js
function power(base, exp = 2) {
  return base ** exp;
}
power(3);      // 9
power(2, 10);  // 1024

function sum(...nums) {          // rest: массив аргументов
  return nums.reduce((a, b) => a + b, 0);
}
sum(1, 2, 3, 4);   // 10
```

## Возврат значения
Без `return` функция возвращает `undefined`. После `return` код не выполняется.
```js
function minMax(arr) {
  return { min: Math.min(...arr), max: Math.max(...arr) };
}
const { min, max } = minMax([3, 1, 8]);
```

## Функции как значения
```js
function apply(fn, value) {
  return fn(value);
}
apply(square, 5);          // 25
```

## Рекурсия
```js
function factorial(n) {
  return n <= 1 ? 1 : n * factorial(n - 1);
}
```

## Типичные ошибки
- Вызов без скобок: `greet` вместо `greet()`
- Забыли `return` в функции
- Обращение к параметру, которого не передали (`undefined`)

## Практика
1. `isPrime(n)` — проверка простого числа.
2. `average(...nums)` — среднее значение.
3. `fib(n)` — n-е число Фибоначчи.

## Проверь себя
1. Что возвращает функция без `return`?
2. Что такое hoisting?
3. Для чего нужен rest-параметр `...args`?

---
[← Урок 5](lesson-05.md) · [Программа курса](README.md) · [Урок 7 →](lesson-07.md)
