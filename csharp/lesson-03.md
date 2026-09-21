# C# · Урок 3. Ввод и вывод в консоли

## Цели урока
- Считывать данные пользователя
- Форматировать вывод

## Вывод
```csharp
Console.WriteLine("Строка с переводом");
Console.Write("Без перевода ");
Console.WriteLine();

string name = "Мадина";
int age = 19;
Console.WriteLine("Имя: " + name);
Console.WriteLine($"Имя: {name}, возраст: {age}");           // интерполяция
Console.WriteLine("Имя: {0}, возраст: {1}", name, age);       // составное форматирование
```

## Ввод
`Console.ReadLine()` возвращает строку (или `null`).
```csharp
Console.Write("Как вас зовут? ");
string? input = Console.ReadLine();
string userName = string.IsNullOrWhiteSpace(input) ? "Гость" : input;

Console.Write("Возраст: ");
if (int.TryParse(Console.ReadLine(), out int years))
    Console.WriteLine($"Через 5 лет вам будет {years + 5}");
else
    Console.WriteLine("Это не число");
```

## Форматирование чисел
```csharp
double pi = 3.14159265;
Console.WriteLine($"{pi:F2}");             // 3.14
Console.WriteLine($"{1234567.891:N2}");    // 1 234 567,89
Console.WriteLine($"{0.256:P1}");          // 25,6 %
Console.WriteLine($"{1500:C}");            // валюта
Console.WriteLine($"{42,8}|{42,-8}|");     // выравнивание
Console.WriteLine($"{255:X}");             // FF
Console.WriteLine($"{7:D3}");              // 007
```

## Кодировка и цвета
```csharp
Console.OutputEncoding = System.Text.Encoding.UTF8;    // русский и таджикский текст
Console.ForegroundColor = ConsoleColor.Green;
Console.WriteLine("Зелёный текст");
Console.ResetColor();
```

## Чтение клавиш
```csharp
Console.WriteLine("Нажмите любую клавишу...");
Console.ReadKey();
```

## Типичные ошибки
- `Console.ReadLine()` может вернуть `null` (Ctrl+Z) — учитывайте
- Прямое `int.Parse(Console.ReadLine())` падает на некорректном вводе
- Проблемы с кодировкой в консоли Windows — задайте `UTF8`

## Практика
1. Считайте два числа, выведите сумму, разность, произведение, частное (2 знака).
2. Считайте имя, город и год рождения, выведите красивую визитку.
3. Выведите таблицу цен с выравниванием по столбцам.

## Проверь себя
1. Что возвращает `ReadLine`?
2. Как вывести число с двумя знаками после запятой?
3. Что такое интерполяция строк?

---
[← Урок 2](lesson-02.md) · [Программа курса](README.md) · [Урок 4 →](lesson-04.md)
