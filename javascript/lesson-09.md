# JavaScript · Урок 9. Методы массивов: map, filter, reduce

## Цели урока
- Преобразовывать данные без ручных циклов

## map — преобразовать каждый элемент
```js
const prices = [100, 250, 400];
const withTax = prices.map(p => p * 1.1);    // новый массив
const names = users.map(u => u.name);
```

## filter — оставить подходящие
```js
const expensive = prices.filter(p => p > 200);   // [250, 400]
const adults = users.filter(u => u.age >= 18);
```

## reduce — свести к одному значению
```js
const total = prices.reduce((sum, p) => sum + p, 0);    // 750
const maxPrice = prices.reduce((m, p) => (p > m ? p : m), prices[0]);

const counts = ["a", "b", "a"].reduce((acc, ch) => {
  acc[ch] = (acc[ch] || 0) + 1;
  return acc;
}, {});   // { a: 2, b: 1 }
```

## some, every, find
```js
prices.some(p => p > 300);    // есть ли хоть один
prices.every(p => p > 50);    // все ли подходят
```

## Цепочки методов
```js
const result = users
  .filter(u => u.age >= 18)
  .map(u => u.name.toUpperCase())
  .sort();
```

## Другие полезные
```js
[1, [2, [3]]].flat(Infinity);            // [1, 2, 3]
Array.from({ length: 5 }, (_, i) => i);  // [0, 1, 2, 3, 4]
Object.entries({ a: 1 });                // [["a", 1]]
```

## Типичные ошибки
- Забыли начальное значение у `reduce` (`0`) — падает на пустом массиве
- `map` без `return` в фигурных скобках даёт массив `undefined`
- `forEach` не возвращает результат — для преобразований берите `map`

## Практика
1. Из массива объектов `{name, price}` получите общую стоимость.
2. Получите список уникальных слов из предложения, отсортированный по алфавиту.
3. Посчитайте частоту каждого слова через `reduce`.

## Проверь себя
1. Чем `map` отличается от `forEach`?
2. Что делает `reduce`?
3. Что вернёт `[].every(x => x > 5)`?

---
[← Урок 8](lesson-08.md) · [Программа курса](README.md) · [Урок 10 →](lesson-10.md)
