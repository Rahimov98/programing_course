# C# · Урок 6. Циклы

## Цели урока
- Повторять действия: `for`, `while`, `do-while`, `foreach`

## for
```csharp
for (int i = 0; i < 5; i++)
    Console.Write(i + " ");          // 0 1 2 3 4
```

## while и do-while
```csharp
int n = 5;
while (n > 0)
{
    Console.Write(n-- + " ");
}

string? input;
do
{
    Console.Write("Введите 'ok': ");
    input = Console.ReadLine();
} while (input != "ok");
```

## foreach
```csharp
string[] names = { "Али", "Мадина", "Фируз" };
foreach (string name in names)
    Console.WriteLine(name);
```
Внутри `foreach` нельзя изменять коллекцию.

## break и continue
```csharp
for (int i = 1; i <= 10; i++)
{
    if (i % 2 == 0) continue;     // пропуск чётных
    if (i > 7) break;             // выход
    Console.Write(i + " ");       // 1 3 5 7
}
```

## Вложенные циклы
```csharp
for (int i = 1; i <= 5; i++)
{
    for (int j = 1; j <= i; j++) Console.Write("*");
    Console.WriteLine();
}
```

## Примеры
```csharp
// сумма цифр
int num = 12345, sum = 0;
while (num > 0) { sum += num % 10; num /= 10; }

// факториал
long fact = 1;
for (int i = 2; i <= 10; i++) fact *= i;

// угадай число
var rnd = new Random();
int secret = rnd.Next(1, 21), guess;
do
{
    Console.Write("Ваш вариант: ");
    guess = int.Parse(Console.ReadLine()!);
    Console.WriteLine(guess < secret ? "Больше" : guess > secret ? "Меньше" : "Угадали!");
} while (guess != secret);
```

## Типичные ошибки
- Бесконечный цикл (нет изменения счётчика)
- Выход за границы массива при `i <= arr.Length`
- Изменение коллекции в `foreach` → `InvalidOperationException`

## Практика
1. Выведите таблицу умножения.
2. Найдите все простые числа до 100.
3. Выведите числа Фибоначчи до 1000.

## Проверь себя
1. Когда `foreach` удобнее `for`?
2. Чем `while` отличается от `do-while`?
3. Что делает `continue`?

---
[← Урок 5](lesson-05.md) · [Программа курса](README.md) · [Урок 7 →](lesson-07.md)
