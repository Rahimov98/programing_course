# C# · Урок 13. Наследование

## Цели урока
- Создавать иерархии классов
- Использовать `base`, `protected`, `sealed`

## Наследование
```csharp
class Animal
{
    public string Name { get; }
    protected int energy = 100;

    public Animal(string name) { Name = name; }

    public void Eat() => energy += 10;
    public virtual string Speak() => "...";
}

class Dog : Animal
{
    public string Breed { get; }

    public Dog(string name, string breed) : base(name)     // вызов конструктора базового
    {
        Breed = breed;
    }

    public override string Speak() => $"{Name}: Гав!";
    public void Fetch() { energy -= 5; }
}

class Cat : Animal
{
    public Cat(string name) : base(name) { }
    public override string Speak() => $"{Name}: Мяу!";
}

Animal[] pets = { new Dog("Рекс", "овчарка"), new Cat("Мурка") };
foreach (var p in pets) Console.WriteLine(p.Speak());
```

## Ключевые слова
- `virtual` — метод можно переопределить
- `override` — переопределение
- `base.Method()` — вызвать версию из базового класса
- `sealed` — запретить дальнейшее наследование (класса или метода)
- `new` — скрыть метод базового класса (использовать редко)

```csharp
public override string ToString() => $"{base.ToString()} + свои данные";
```

## Проверка типа
```csharp
if (pet is Dog d) d.Fetch();
Animal a = new Dog("Рекс", "овчарка");
Dog? dog = a as Dog;              // null, если не подходит
```

## Все классы наследуют `object`
Методы `ToString()`, `Equals()`, `GetHashCode()` можно переопределять.

## Композиция или наследование?
- «Является» (Dog is an Animal) → наследование
- «Имеет» (Car has an Engine) → поле-объект (композиция)

C# поддерживает только одиночное наследование классов (но много интерфейсов).

## Типичные ошибки
- Забыли `virtual` в базовом методе — переопределить нельзя
- Не вызвали `base(...)`, когда у базового нет конструктора без параметров
- Слишком глубокие иерархии

## Практика
1. Иерархия `Shape` → `Circle`, `Rectangle` с `Area()`.
2. Классы `Employee` → `Manager`, `Developer` с расчётом зарплаты.
3. Переопределите `ToString()` и `Equals()` в своём классе.

## Проверь себя
1. Чем `virtual` отличается от `override`?
2. Что делает `base`?
3. Зачем нужен `sealed`?

---
[← Урок 12](lesson-12.md) · [Программа курса](README.md) · [Урок 14 →](lesson-14.md)
