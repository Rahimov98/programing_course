# C# · Урок 12. Свойства и конструкторы

## Цели урока
- Использовать свойства вместо публичных полей
- Знать виды конструкторов и инициализаторов

## Свойства
```csharp
class Student
{
    private int age;

    public string Name { get; set; } = "";        // автосвойство
    public int Id { get; }                         // только для чтения
    public string Group { get; private set; } = "A-101";

    public int Age
    {
        get => age;
        set
        {
            if (value < 0 || value > 120)
                throw new ArgumentOutOfRangeException(nameof(value));
            age = value;
        }
    }

    public bool IsAdult => Age >= 18;              // вычисляемое свойство
    public required string Email { get; init; }    // C# 11: обязательное; init — задать только при создании
}
```

## Конструкторы
```csharp
class Person
{
    public string Name { get; }
    public int Age { get; }

    public Person() : this("Без имени", 0) { }                // делегирование
    public Person(string name) : this(name, 18) { }
    public Person(string name, int age)
    {
        Name = name;
        Age = age;
    }
}

var a = new Person();
var b = new Person("Али", 21);
```

## Инициализатор объекта
```csharp
var s = new Student { Name = "Мадина", Age = 19, Email = "m@mail.com" };
```

## Первичный конструктор (C# 12)
```csharp
class Product(string name, decimal price)
{
    public string Name { get; } = name;
    public decimal Price { get; } = price;
}
```

## Статический конструктор и индексатор
```csharp
class Playlist
{
    private readonly List<string> songs = new();
    public string this[int i] => songs[i];     // индексатор
    public void Add(string s) => songs.Add(s);
}
```

## readonly
Поле `readonly` можно задать только в конструкторе.

## Типичные ошибки
- Публичные поля вместо свойств
- Логика проверки в конструкторе и в свойстве продублирована
- Бесконечная рекурсия: `set { Age = value; }` внутри самого свойства `Age`

## Практика
1. Класс `Temperature` со свойствами `Celsius` и вычисляемым `Fahrenheit`.
2. Класс `Employee` с проверкой зарплаты `> 0`.
3. Класс с индексатором для хранения оценок по предметам.

## Проверь себя
1. Что такое автосвойство?
2. Зачем нужен модификатор `init`?
3. Как вызвать один конструктор из другого?

---
[← Урок 11](lesson-11.md) · [Программа курса](README.md) · [Урок 13 →](lesson-13.md)
