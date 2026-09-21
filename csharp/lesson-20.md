# C# · Урок 20. Делегаты, события, лямбды

## Цели урока
- Передавать методы как параметры
- Создавать и обрабатывать события

## Делегаты
Тип, описывающий сигнатуру метода:
```csharp
delegate int Operation(int a, int b);

static int Add(int a, int b) => a + b;
static int Mul(int a, int b) => a * b;

Operation op = Add;
Console.WriteLine(op(2, 3));       // 5
op = Mul;
Console.WriteLine(op(2, 3));       // 6
```

## Встроенные делегаты
```csharp
Func<int, int, int> add = (a, b) => a + b;      // принимает параметры, возвращает значение
Action<string> print = s => Console.WriteLine(s);  // ничего не возвращает
Predicate<int> isEven = n => n % 2 == 0;          // возвращает bool

Console.WriteLine(add(2, 3));
print("Привет");
```

## Лямбда-выражения
```csharp
Func<int, int> square = x => x * x;
Func<int, int, int> sum = (a, b) => a + b;
Action greet = () => Console.WriteLine("Hi");
Func<int, string> describe = n =>
{
    if (n < 0) return "отрицательное";
    return n == 0 ? "ноль" : "положительное";
};
```

## Методы, принимающие функции
```csharp
static void Repeat(int times, Action action)
{
    for (int i = 0; i < times; i++) action();
}
Repeat(3, () => Console.WriteLine("Привет"));

static List<T> Filter<T>(List<T> list, Func<T, bool> predicate)
{
    var result = new List<T>();
    foreach (var x in list) if (predicate(x)) result.Add(x);
    return result;
}
```

## Мультикаст
```csharp
Action notify = () => Console.WriteLine("Первый");
notify += () => Console.WriteLine("Второй");
notify();                           // вызовет оба
```

## События
Механизм оповещения подписчиков:
```csharp
class Button
{
    public event EventHandler? Clicked;
    public event Action<string>? Message;

    public void Click()
    {
        Console.WriteLine("Кнопка нажата");
        Clicked?.Invoke(this, EventArgs.Empty);
        Message?.Invoke("Привет из кнопки");
    }
}

var b = new Button();
b.Clicked += (s, e) => Console.WriteLine("Подписчик 1");
b.Clicked += (s, e) => Console.WriteLine("Подписчик 2");
b.Message += text => Console.WriteLine(text);
b.Click();
```
Событие можно вызвать только внутри класса-владельца; снаружи — только `+=` и `-=`.

## Пример: банковский счёт
```csharp
class Account
{
    public decimal Balance { get; private set; }
    public event Action<decimal>? LowBalance;

    public void Withdraw(decimal amount)
    {
        Balance -= amount;
        if (Balance < 100) LowBalance?.Invoke(Balance);
    }
}
```

## Типичные ошибки
- Вызов события без `?.` → `NullReferenceException` при отсутствии подписчиков
- Забыли отписаться (`-=`) — утечка памяти
- Захват изменяемой переменной цикла в лямбде

## Практика
1. Метод `Apply(int[] a, Func<int,int> f)`, применяющий функцию к каждому элементу.
2. Событие `TemperatureChanged` в классе `Thermostat`.
3. Калькулятор, хранящий операции в `Dictionary<string, Func<double, double, double>>`.

## Проверь себя
1. Чем `Func` отличается от `Action`?
2. Как работает событие?
3. Что такое лямбда-выражение?

---
[← Урок 19](lesson-19.md) · [Программа курса](README.md) · [Урок 21 →](lesson-21.md)
