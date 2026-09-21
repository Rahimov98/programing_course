# C# · Урок 19. LINQ

## Цели урока
- Запрашивать и преобразовывать коллекции декларативно

## Основы
LINQ (Language Integrated Query) — методы для работы с любыми последовательностями. Нужно `using System.Linq;` (в новых проектах подключён автоматически).

```csharp
int[] nums = { 5, 2, 8, 1, 9, 3, 7 };

var evens   = nums.Where(n => n % 2 == 0);
var squares = nums.Select(n => n * n);
var sorted  = nums.OrderBy(n => n);
var desc    = nums.OrderByDescending(n => n);
var top3    = nums.OrderByDescending(n => n).Take(3);
var skip2   = nums.Skip(2);

nums.Sum(); nums.Average(); nums.Min(); nums.Max(); nums.Count();
nums.Any(n => n > 8);      // есть хотя бы один
nums.All(n => n > 0);      // все подходят
nums.First(n => n > 5);    // бросает исключение, если нет
nums.FirstOrDefault(n => n > 100);   // 0, если нет
nums.Distinct();
nums.ToList(); nums.ToArray();
```

## Работа с объектами
```csharp
record Student(string Name, string Group, double Gpa);

var students = new List<Student>
{
    new("Али", "A", 4.5), new("Мадина", "A", 4.8),
    new("Фируз", "B", 3.9), new("Дилноза", "B", 4.2)
};

var best = students.Where(s => s.Gpa >= 4.0)
                   .OrderByDescending(s => s.Gpa)
                   .Select(s => s.Name);
Console.WriteLine(string.Join(", ", best));
```

## GroupBy
```csharp
foreach (var g in students.GroupBy(s => s.Group))
{
    Console.WriteLine($"Группа {g.Key}: средний балл {g.Average(s => s.Gpa):F2}");
    foreach (var s in g) Console.WriteLine($"  {s.Name}");
}
```

## Синтаксис запросов
```csharp
var q = from s in students
        where s.Gpa > 4
        orderby s.Name
        select new { s.Name, s.Gpa };
```

## Соединение
```csharp
var joined = students.Join(groups, s => s.Group, g => g.Code, (s, g) => new { s.Name, g.Title });
```

## Отложенное выполнение
Запрос выполняется не при создании, а при переборе. Если нужен «снимок» — вызовите `.ToList()`.
```csharp
var numbers = new List<int> { 1, 5, 9 };
var query = numbers.Where(n => n > 3);   // запрос ещё не выполнялся
numbers.Add(7);                          // источник изменился до перебора
var list = query.ToList();               // выполнилось здесь: 5, 9, 7
```

## Типичные ошибки
- `First()` на пустой последовательности → исключение
- Многократный перебор дорогого запроса — сохраните в `ToList()`
- Изменение коллекции во время выполнения запроса

## Практика
1. Найдите студентов со средним баллом выше среднего по группе.
2. Получите топ-3 самых длинных слова в тексте.
3. Сгруппируйте слова по первой букве и выведите количество в каждой группе.

## Проверь себя
1. Чем `Select` отличается от `Where`?
2. Что такое отложенное выполнение?
3. Чем `First` отличается от `FirstOrDefault`?

---
[← Урок 18](lesson-18.md) · [Программа курса](README.md) · [Урок 20 →](lesson-20.md)
