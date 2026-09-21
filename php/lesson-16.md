# PHP · Урок 16. Наследование, интерфейсы, трейты

## Цели урока
- Наследовать классы
- Реализовывать интерфейсы
- Использовать трейты для переиспользования кода

## Теория

**Наследование**
```php
class Animal {
    public function __construct(public string $name) {}

    public function speak(): string {
        return "...";
    }
}

class Dog extends Animal {
    public function speak(): string {
        return "Гав!";
    }
}

$dog = new Dog("Бобик");
echo $dog->speak();  // Гав!
```

**parent::**
```php
class Cat extends Animal {
    public function speak(): string {
        return parent::speak() . " Мяу!";
    }
}
```

**Абстрактный класс**
```php
abstract class Shape {
    abstract public function area(): float;

    public function description(): string {
        return "Площадь: " . $this->area();
    }
}

class Circle extends Shape {
    public function __construct(private float $r) {}
    public function area(): float {
        return pi() * $this->r ** 2;
    }
}
```

**Интерфейс**
```php
interface Loggable {
    public function log(string $message): void;
}

class FileLogger implements Loggable {
    public function log(string $message): void {
        file_put_contents("app.log", $message . "\n", FILE_APPEND);
    }
}
```

**Трейт**
```php
trait Timestampable {
    public function createdAt(): string {
        return date("Y-m-d H:i:s");
    }
}

class Post {
    use Timestampable;
}
```

## Типичные ошибки
- Множественное наследование классов запрещено (только через интерфейсы/трейты)
- Забыли реализовать все методы интерфейса
- Конфликт имён методов в нескольких трейтах

## Практика
1. Классы `Vehicle` → `Car`, `Bike` с методом `move()`.
2. Интерфейс `Payable` с методом `pay($amount)`.
3. Трейт `Identifiable` с полем `id` и геттером.

## Проверь себя
1. Чем интерфейс отличается от абстрактного класса?
2. Зачем нужны трейты?
3. Можно ли наследовать несколько классов?

---
[← Урок 15](lesson-15.md) · [Программа курса](README.md) · [Урок 17 →](lesson-17.md)
