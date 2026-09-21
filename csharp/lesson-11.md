# C# · Урок 11. Классы и объекты

## Цели урока
- Описывать классы с полями и методами
- Использовать модификаторы доступа

## Класс
```csharp
class BankAccount
{
    private decimal balance;              // поле
    public string Owner { get; }          // свойство (подробнее в след. уроке)

    public BankAccount(string owner, decimal initial = 0)
    {
        Owner = owner;
        balance = initial;
    }

    public void Deposit(decimal amount)
    {
        if (amount <= 0) throw new ArgumentException("Сумма должна быть положительной");
        balance += amount;
    }

    public bool Withdraw(decimal amount)
    {
        if (amount <= 0 || amount > balance) return false;
        balance -= amount;
        return true;
    }

    public decimal GetBalance() => balance;

    public override string ToString() => $"{Owner}: {balance:C}";
}

var acc = new BankAccount("Алишер", 1000);
acc.Deposit(500);
Console.WriteLine(acc);
```

## Модификаторы доступа
- `public` — доступно всем
- `private` — только внутри класса (по умолчанию для членов)
- `protected` — внутри класса и наследников
- `internal` — внутри сборки (проекта)

## Статические члены
```csharp
class Counter
{
    public static int Count { get; private set; }
    public Counter() { Count++; }
    public static void Reset() => Count = 0;
}
new Counter(); new Counter();
Console.WriteLine(Counter.Count);       // 2
```

## Файлы классов
Принято хранить каждый класс в отдельном файле `BankAccount.cs`. Классы в одном пространстве имён видны друг другу.

## record
Неизменяемый тип данных с автоматическим `Equals` и `ToString`:
```csharp
record Point(int X, int Y);
var p = new Point(1, 2);
var p2 = p with { X = 5 };
```

## Ссылочные и значимые типы
`class` — ссылочный тип (переменная хранит ссылку), `struct` — значимый (копируется).

## Типичные ошибки
- Публичные поля вместо свойств
- Забыли `new` при создании объекта
- Обращение к объекту, равному `null` → `NullReferenceException`

## Практика
1. Класс `Rectangle` с методами `Area()`, `Perimeter()`.
2. Класс `Book` с проверкой года издания.
3. Класс `Counter` с методами `Increment`, `Decrement`, `Reset`.

## Проверь себя
1. Что такое модификатор `private`?
2. Чем `class` отличается от `struct`?
3. Что такое `record`?

---
[← Урок 10](lesson-10.md) · [Программа курса](README.md) · [Урок 12 →](lesson-12.md)
