# JavaScript · Урок 15. Классы и ООП

## Цели урока
- Создавать классы, наследовать, использовать геттеры и приватные поля

## Класс
```js
class Student {
  #grades = [];                       // приватное поле

  constructor(name, age) {
    this.name = name;
    this.age = age;
  }

  addGrade(g) {
    if (g < 1 || g > 5) throw new Error("Оценка от 1 до 5");
    this.#grades.push(g);
  }

  get average() {
    if (!this.#grades.length) return 0;
    return this.#grades.reduce((a, b) => a + b) / this.#grades.length;
  }

  toString() {
    return `${this.name} (${this.age})`;
  }

  static create(name) {
    return new Student(name, 18);
  }
}

const s = new Student("Алишер", 21);
s.addGrade(5);
s.addGrade(4);
console.log(s.average);      // 4.5 (геттер, вызывается без скобок)
console.log(`${s}`);
```

## Наследование
```js
class Animal {
  constructor(name) { this.name = name; }
  speak() { return `${this.name} издаёт звук`; }
}

class Dog extends Animal {
  constructor(name, breed) {
    super(name);                 // вызов конструктора родителя
    this.breed = breed;
  }
  speak() { return `${this.name} лает`; }   // переопределение
}

const d = new Dog("Рекс", "овчарка");
console.log(d.speak(), d instanceof Animal);   // true
```

## Полезное
- `static` — метод класса, вызывается без создания объекта
- `#field` — по-настоящему приватное поле
- `get` / `set` — свойства с логикой

## Типичные ошибки
- Забыли `new` при создании объекта
- В конструкторе наследника обратились к `this` до `super()`
- Потерян `this` при передаче метода как колбэка — используйте стрелочную функцию или `.bind(this)`

## Практика
1. Класс `Rectangle` с методами `area()`, `perimeter()`.
2. Класс `BankAccount` с приватным балансом и методами `deposit`, `withdraw`.
3. Иерархия `Shape` → `Circle`, `Square` с общим методом `area()`.

## Проверь себя
1. Для чего нужен `super`?
2. Чем `static` метод отличается от обычного?
3. Как сделать поле приватным?

---
[← Урок 14](lesson-14.md) · [Программа курса](README.md) · [Урок 16 →](lesson-16.md)
