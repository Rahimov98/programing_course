# C# · Урок 10. Коллекции: List и Dictionary

## Цели урока
- Использовать динамические коллекции

## List<T>
```csharp
var nums = new List<int> { 5, 2, 9 };
nums.Add(7);
nums.AddRange(new[] { 1, 3 });
nums.Insert(0, 100);
nums.Remove(9);          // по значению
nums.RemoveAt(0);        // по индексу
nums.Contains(5);
nums.IndexOf(7);
nums.Sort();
nums.Reverse();
Console.WriteLine(nums.Count);

foreach (var n in nums) Console.Write(n + " ");
nums.RemoveAll(x => x % 2 == 0);
```

## Dictionary<TKey, TValue>
```csharp
var ages = new Dictionary<string, int>
{
    ["Али"] = 21,
    ["Мадина"] = 19
};
ages["Фируз"] = 22;
ages.Add("Дилноза", 20);

if (ages.TryGetValue("Али", out int age))
    Console.WriteLine(age);

ages.ContainsKey("Мадина");
ages.Remove("Фируз");

foreach (var (name, a) in ages)
    Console.WriteLine($"{name}: {a}");
```

## HashSet<T>
```csharp
var set = new HashSet<int> { 1, 2, 2, 3 };    // 1, 2, 3
set.Add(5);
set.UnionWith(new[] { 7, 8 });
set.Contains(2);
```

## Queue и Stack
```csharp
var q = new Queue<string>();
q.Enqueue("a"); q.Enqueue("b");
q.Dequeue();          // "a" (первый вошёл — первый вышел)

var st = new Stack<int>();
st.Push(1); st.Push(2);
st.Pop();             // 2 (последний вошёл — первый вышел)
st.Peek();
```

## Подсчёт слов
```csharp
var freq = new Dictionary<string, int>();
foreach (var w in text.Split(' '))
    freq[w] = freq.GetValueOrDefault(w) + 1;
```

## Типичные ошибки
- `dict["нет"]` бросает `KeyNotFoundException` — используйте `TryGetValue`
- Изменение списка внутри `foreach`
- `Remove` возвращает `bool` — не проверяют результат

## Практика
1. Прочитайте числа в `List<int>`, выведите отсортированными и их сумму.
2. Подсчитайте частоту слов в тексте.
3. Проверка скобок в выражении с помощью `Stack<char>`.

## Проверь себя
1. Чем `List` отличается от массива?
2. Как безопасно получить значение из словаря?
3. Чем `Queue` отличается от `Stack`?

---
[← Урок 9](lesson-09.md) · [Программа курса](README.md) · [Урок 11 →](lesson-11.md)
