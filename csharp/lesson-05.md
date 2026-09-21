# C# · Урок 5. Условия: if / else и switch

## Цели урока
- Управлять ходом программы

## if / else
```csharp
Console.Write("Возраст: ");
int age = int.Parse(Console.ReadLine()!);

if (age < 12)
    Console.WriteLine("Ребёнок");
else if (age < 18)
    Console.WriteLine("Подросток");
else if (age < 65)
    Console.WriteLine("Взрослый");
else
    Console.WriteLine("Пожилой");
```
Для нескольких инструкций используйте `{ }`.

## switch (классический)
```csharp
Console.Write("Номер дня (1-7): ");
int day = int.Parse(Console.ReadLine()!);

switch (day)
{
    case 1:
        Console.WriteLine("Понедельник");
        break;
    case 6:
    case 7:
        Console.WriteLine("Выходной");
        break;
    default:
        Console.WriteLine("Будний день");
        break;
}
```
В C# каждая ветка должна заканчиваться `break` (или `return`) — «проваливания» нет.

## switch-выражение (C# 8+)
```csharp
string name = day switch
{
    1 => "Понедельник",
    2 => "Вторник",
    3 => "Среда",
    >= 4 and <= 5 => "Четверг или пятница",
    6 or 7 => "Выходной",
    _ => "Нет такого дня"
};
```

## Сопоставление с образцом
```csharp
object o = 42;
if (o is int n && n > 10)
    Console.WriteLine($"Целое число больше 10: {n}");

string category = age switch
{
    < 12 => "ребёнок",
    < 18 => "подросток",
    _ => "взрослый"
};
```

## Типичные ошибки
- `;` после `if (...)`
- Отсутствие `break` в `case`
- Сравнение строк без учёта регистра: используйте `string.Equals(a, b, StringComparison.OrdinalIgnoreCase)`

## Практика
1. Калькулятор: два числа и операция (`+ - * /`) через `switch`; деление на ноль.
2. Определите, високосный ли год.
3. Программа выставляет оценку по баллам через switch-выражение.

## Проверь себя
1. Чем switch-выражение отличается от оператора?
2. Зачем `break` в `case`?
3. Что означает `_` в `switch`?

---
[← Урок 4](lesson-04.md) · [Программа курса](README.md) · [Урок 6 →](lesson-06.md)
