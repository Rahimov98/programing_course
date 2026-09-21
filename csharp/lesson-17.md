# C# · Урок 17. Обработка исключений

## Цели урока
- Перехватывать и выбрасывать исключения
- Создавать собственные типы исключений

## try / catch / finally
```csharp
try
{
    Console.Write("Число: ");
    int n = int.Parse(Console.ReadLine()!);
    Console.WriteLine(100 / n);
}
catch (FormatException)
{
    Console.WriteLine("Это не число");
}
catch (DivideByZeroException ex)
{
    Console.WriteLine($"Деление на ноль: {ex.Message}");
}
catch (Exception ex)
{
    Console.WriteLine($"Неожиданная ошибка: {ex.Message}");
}
finally
{
    Console.WriteLine("Выполняется всегда");
}
```
Порядок `catch`: сначала конкретные, затем общие.

## Фильтры исключений
```csharp
catch (HttpRequestException ex) when (ex.StatusCode == System.Net.HttpStatusCode.NotFound)
{
    Console.WriteLine("Не найдено");
}
```

## throw
```csharp
static void SetAge(int age)
{
    if (age < 0) throw new ArgumentOutOfRangeException(nameof(age), "Возраст не может быть отрицательным");
}

static void Process()
{
    try { /* ... */ }
    catch (Exception)
    {
        // логирование
        throw;              // пробросить дальше с сохранением стека
    }
}
```
Используйте `throw;`, а не `throw ex;` — иначе теряется стек вызовов.

## Собственные исключения
```csharp
class InsufficientFundsException : Exception
{
    public decimal Needed { get; }

    public InsufficientFundsException(decimal needed)
        : base($"Не хватает {needed:C}") { Needed = needed; }
}

try { throw new InsufficientFundsException(150); }
catch (InsufficientFundsException ex) { Console.WriteLine(ex.Needed); }
```

## using и освобождение ресурсов
```csharp
using var reader = new StreamReader("file.txt");   // Dispose() при выходе из блока
```

## Проверка аргументов
```csharp
ArgumentNullException.ThrowIfNull(name);
ArgumentException.ThrowIfNullOrEmpty(name);
```

## Частые исключения
`NullReferenceException`, `IndexOutOfRangeException`, `InvalidCastException`, `FormatException`, `FileNotFoundException`, `InvalidOperationException`, `ArgumentException`.

## Типичные ошибки
- `catch (Exception)` с пустым телом — «глотает» ошибку
- Исключения как способ обычного управления потоком
- `throw ex;` вместо `throw;`

## Практика
1. Безопасный калькулятор без падений.
2. Исключение `InvalidEmailException` для проверки почты.
3. Чтение файла с обработкой `FileNotFoundException` и `UnauthorizedAccessException`.

## Проверь себя
1. Когда выполняется `finally`?
2. Чем `throw;` отличается от `throw ex;`?
3. Как создать своё исключение?

---
[← Урок 16](lesson-16.md) · [Программа курса](README.md) · [Урок 18 →](lesson-18.md)
