# C# · Урок 8. Массивы

## Цели урока
- Работать с одномерными и двумерными массивами
- Использовать методы класса `Array`

## Одномерные
```csharp
int[] nums = new int[5];                 // пять нулей
int[] a = { 10, 20, 30, 40, 50 };
string[] names = new[] { "Али", "Мадина" };

a[0] = 99;
Console.WriteLine(a.Length);             // 5
Console.WriteLine(a[^1]);                // последний элемент (50)
int[] part = a[1..4];                    // срез: 20, 30, 40
```

## Перебор
```csharp
for (int i = 0; i < a.Length; i++) Console.Write(a[i] + " ");
foreach (int v in a) Console.Write(v + " ");
```

## Класс Array
```csharp
Array.Sort(a);
Array.Reverse(a);
int idx = Array.IndexOf(a, 30);
Array.Resize(ref a, 10);
Array.Copy(a, copy, a.Length);
Array.Clear(a, 0, a.Length);
```

## Методы LINQ (`using System.Linq;`)
```csharp
a.Sum(); a.Average(); a.Min(); a.Max();
a.Where(x => x > 20).ToArray();
a.Contains(30);
```

## Многомерные
```csharp
int[,] m = new int[3, 4];
int[,] init = { { 1, 2 }, { 3, 4 } };
m[1, 2] = 5;

for (int i = 0; i < init.GetLength(0); i++)
{
    for (int j = 0; j < init.GetLength(1); j++)
        Console.Write(init[i, j] + " ");
    Console.WriteLine();
}
```

## Зубчатые массивы
```csharp
int[][] jag = new int[3][];
jag[0] = new[] { 1 };
jag[1] = new[] { 1, 2 };
jag[2] = new[] { 1, 2, 3 };
```

## Типичные ошибки
- `IndexOutOfRangeException` при `i <= a.Length`
- Массив — ссылочный тип: `b = a` не копирует; используйте `(int[])a.Clone()`
- Размер массива менять нельзя (для этого есть `List<T>`)

## Практика
1. Найдите максимум, минимум и среднее массива без LINQ.
2. Циклически сдвиньте массив на 1 элемент.
3. Заполните матрицу 5×5 таблицей умножения.

## Проверь себя
1. Что означает `a[^1]`?
2. Чем `int[,]` отличается от `int[][]`?
3. Почему `b = a` не создаёт копию?

---
[← Урок 7](lesson-07.md) · [Программа курса](README.md) · [Урок 9 →](lesson-09.md)
