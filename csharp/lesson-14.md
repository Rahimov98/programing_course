# C# · Урок 14. Полиморфизм и абстрактные классы

## Цели урока
- Вызывать нужную реализацию через ссылку на базовый класс
- Создавать абстрактные классы и члены

## Полиморфизм
Один вызов — разное поведение в зависимости от реального типа объекта:
```csharp
abstract class Shape
{
    public string Name { get; }
    protected Shape(string name) { Name = name; }

    public abstract double Area();                    // нет реализации — обязаны переопределить
    public virtual void Print() =>
        Console.WriteLine($"{Name}: площадь {Area():F2}");
}

class Circle : Shape
{
    public double R { get; }
    public Circle(double r) : base("Круг") { R = r; }
    public override double Area() => Math.PI * R * R;
}

class Rectangle : Shape
{
    public double W { get; }
    public double H { get; }
    public Rectangle(double w, double h) : base("Прямоугольник") { W = w; H = h; }
    public override double Area() => W * H;
}

Shape[] shapes = { new Circle(2), new Rectangle(3, 4) };
foreach (Shape s in shapes) s.Print();      // вызовутся нужные версии Area()

double total = shapes.Sum(s => s.Area());
```

## Абстрактные классы
- `abstract class` — нельзя создать экземпляр (`new Shape()` — ошибка)
- `abstract` метод — без тела, наследник обязан его реализовать
- Может содержать обычные поля, свойства, методы и конструкторы

## Сравнение с virtual
| | `virtual` | `abstract` |
|---|---|---|
| Реализация в базовом классе | есть | нет |
| Переопределять | по желанию | обязательно |

## Сопоставление с образцом
```csharp
string Describe(Shape s) => s switch
{
    Circle c    => $"Круг радиуса {c.R}",
    Rectangle r => $"Прямоугольник {r.W}x{r.H}",
    _           => "Неизвестная фигура"
};
```

## Пример: расчёт зарплат
```csharp
abstract class Employee
{
    public string Name { get; init; } = "";
    public abstract decimal Salary();
}
class Manager : Employee { public override decimal Salary() => 5000 + 200 * Team; public int Team { get; init; } }
class Developer : Employee { public override decimal Salary() => 4000 + Bonus; public decimal Bonus { get; init; } }
```

## Типичные ошибки
- Попытка создать экземпляр абстрактного класса
- Забыли `override` у наследника — метод скрывает базовый (предупреждение)
- Переопределяют метод, не объявленный `virtual`/`abstract`

## Практика
1. Добавьте класс `Triangle` и найдите фигуру с наибольшей площадью.
2. Иерархия сотрудников с расчётом общего фонда зарплат.
3. Абстрактный класс `Vehicle` с методом `Move()` и наследниками.

## Проверь себя
1. Что такое полиморфизм?
2. Чем абстрактный класс отличается от обычного?
3. Можно ли создать объект абстрактного класса?

---
[← Урок 13](lesson-13.md) · [Программа курса](README.md) · [Урок 15 →](lesson-15.md)
