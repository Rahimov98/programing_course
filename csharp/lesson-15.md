# C# · Урок 15. Интерфейсы

## Цели урока
- Описывать контракты через интерфейсы
- Реализовывать несколько интерфейсов, использовать стандартные интерфейсы .NET

## Интерфейс
Определяет **что** класс умеет, но не **как**:
```csharp
interface IPayment
{
    string Name { get; }
    bool Pay(decimal amount);
}

class CardPayment : IPayment
{
    public string Name => "Банковская карта";
    public bool Pay(decimal amount)
    {
        Console.WriteLine($"Оплата картой: {amount:C}");
        return true;
    }
}

class CashPayment : IPayment
{
    public string Name => "Наличные";
    public bool Pay(decimal amount)
    {
        Console.WriteLine($"Оплата наличными: {amount:C}");
        return true;
    }
}

void Checkout(IPayment method, decimal total) => method.Pay(total);

Checkout(new CardPayment(), 250);
Checkout(new CashPayment(), 100);
```
Имена интерфейсов принято начинать с `I`.

## Несколько интерфейсов
```csharp
class Duck : IFlyable, ISwimmable { /* ... */ }
```

## Реализация по умолчанию (C# 8+)
```csharp
interface ILogger
{
    void Log(string msg);
    void Error(string msg) => Log("ERROR: " + msg);
}
```

## Зачем интерфейсы
- **Слабая связанность:** код зависит от контракта, а не от конкретного класса
- **Подмена реализаций** (например, в тестах)
- **Множественная «реализация»** — класс наследует один класс, но реализует много интерфейсов

## Внедрение зависимости
```csharp
class OrderService
{
    private readonly IPayment payment;
    public OrderService(IPayment payment) { this.payment = payment; }
    public void Process(decimal sum) => payment.Pay(sum);
}
```

## Стандартные интерфейсы
```csharp
class Student : IComparable<Student>
{
    public string Name { get; set; } = "";
    public double Gpa { get; set; }
    public int CompareTo(Student? other) => Gpa.CompareTo(other?.Gpa);
}
var list = new List<Student>(); list.Sort();          // использует IComparable

class Resource : IDisposable
{
    public void Dispose() => Console.WriteLine("Ресурс освобождён");
}
using (var r = new Resource()) { }     // Dispose вызовется автоматически
```
Также: `IEnumerable<T>`, `IEquatable<T>`.

## Типичные ошибки
- Не реализовали все члены интерфейса
- Путаница: интерфейс — контракт, абстрактный класс — частичная реализация
- Интерфейсы «на всякий случай» для каждого класса

## Практика
1. Интерфейс `IShape` с `Area()` и классы фигур.
2. Интерфейс `INotifier` и реализации `EmailNotifier`, `SmsNotifier`.
3. Реализуйте `IComparable<Book>` и отсортируйте список книг по году.

## Проверь себя
1. Чем интерфейс отличается от абстрактного класса?
2. Сколько интерфейсов может реализовать класс?
3. Для чего нужен `IDisposable`?

---
[← Урок 14](lesson-14.md) · [Программа курса](README.md) · [Урок 16 →](lesson-16.md)
