# PHP · Урок 15. ООП: классы и объекты

## Цели урока
- Создавать классы и объекты
- Использовать свойства, методы, конструктор
- Понимать видимость: `public`, `private`, `protected`

## Теория

```php
<?php
class User {
    public string $name;
    private int $age;

    public function __construct(string $name, int $age) {
        $this->name = $name;
        $this->age = $age;
    }

    public function greet(): string {
        return "Привет, я {$this->name}";
    }

    public function getAge(): int {
        return $this->age;
    }

    public function setAge(int $age): void {
        if ($age < 0) {
            throw new InvalidArgumentException("Возраст не может быть отрицательным");
        }
        $this->age = $age;
    }
}

$user = new User("Мадина", 21);
echo $user->greet();
echo $user->getAge();
```

**Свойства и методы**
- `$this` — ссылка на текущий объект
- Конструктор `__construct` вызывается при `new`
- Деструктор `__destruct` — при уничтожении объекта

**Видимость**
- `public` — доступен отовсюду
- `private` — только внутри класса
- `protected` — внутри класса и наследников

**Статические члены**
```php
class Counter {
    public static int $count = 0;

    public static function increment(): void {
        self::$count++;
    }
}

Counter::increment();
echo Counter::$count;  // 1
```

## Типичные ошибки
- Обращение к `private` свойству снаружи
- Забыли `$this->`
- Создание объекта без `new`

## Практика
1. Класс `Product` с полями `name`, `price` и методом `getInfo()`.
2. Класс `BankAccount` с `private $balance`, методами `deposit` и `withdraw`.
3. Создайте 2–3 объекта и вызовите методы.

## Проверь себя
1. Чем класс отличается от объекта?
2. Зачем `private`?
3. Что такое `$this`?

---
[← Урок 14](lesson-14.md) · [Программа курса](README.md) · [Урок 16 →](lesson-16.md)
