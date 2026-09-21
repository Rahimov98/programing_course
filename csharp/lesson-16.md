# C# · Урок 16. Обобщения (generics)

## Цели урока
- Писать универсальные классы и методы
- Ограничивать типовые параметры

## Обобщённый метод
```csharp
static void Swap<T>(ref T a, ref T b)
{
    (a, b) = (b, a);
}

int x = 1, y = 2;
Swap(ref x, ref y);
string s1 = "a", s2 = "b";
Swap(ref s1, ref s2);

static T Max<T>(T a, T b) where T : IComparable<T> =>
    a.CompareTo(b) >= 0 ? a : b;

Console.WriteLine(Max(3, 7));
Console.WriteLine(Max("яблоко", "груша"));
```

## Обобщённый класс
```csharp
class Stack<T>
{
    private readonly List<T> items = new();

    public void Push(T item) => items.Add(item);

    public T Pop()
    {
        if (items.Count == 0) throw new InvalidOperationException("Стек пуст");
        T item = items[^1];
        items.RemoveAt(items.Count - 1);
        return item;
    }

    public bool IsEmpty => items.Count == 0;
    public int Count => items.Count;
}

var st = new Stack<string>();
st.Push("a"); st.Push("b");
Console.WriteLine(st.Pop());
```

## Ограничения (where)
```csharp
where T : class               // ссылочный тип
where T : struct              // значимый тип
where T : new()               // есть конструктор без параметров
where T : IComparable<T>      // реализует интерфейс
where T : Animal              // наследник класса
```

## Несколько параметров
```csharp
class Pair<TKey, TValue>
{
    public TKey Key { get; }
    public TValue Value { get; }
    public Pair(TKey key, TValue value) { Key = key; Value = value; }
}
var p = new Pair<string, int>("возраст", 21);
```

## Обобщённый репозиторий
```csharp
interface IEntity { int Id { get; } }

class Repository<T> where T : IEntity
{
    private readonly List<T> items = new();
    public void Add(T item) => items.Add(item);
    public T? GetById(int id) => items.FirstOrDefault(x => x.Id == id);
    public IEnumerable<T> GetAll() => items;
}
```

## Ковариантность
`IEnumerable<Dog>` можно присвоить `IEnumerable<Animal>` (только для чтения).

## Типичные ошибки
- Вызов метода, которого нет у `T` без ограничения
- Использование `object` вместо generics (лишние приведения и «упаковка»)
- `new T()` без ограничения `where T : new()`

## Практика
1. Обобщённый метод `IndexOf<T>(T[] arr, T item)`.
2. Класс `Queue<T>` на основе `List<T>`.
3. `Repository<Student>` с поиском по `Id`.

## Проверь себя
1. Чем generics лучше `object`?
2. Что делает `where T : class`?
3. Как ограничить `T` типами, умеющими сравниваться?

---
[← Урок 15](lesson-15.md) · [Программа курса](README.md) · [Урок 17 →](lesson-17.md)
