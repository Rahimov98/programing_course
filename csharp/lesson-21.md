# C# · Урок 21. async / await

## Цели урока
- Выполнять долгие операции без блокировки программы

## Проблема
Обращение к файлам, сети и базам данных занимает время. Если делать это синхронно, программа (или окно) «замирает».

## Task и await
```csharp
static async Task<string> LoadAsync()
{
    await Task.Delay(2000);                // «ждём» без блокировки потока
    return "Данные загружены";
}

Console.WriteLine("Начали");
string result = await LoadAsync();
Console.WriteLine(result);
```
- `async` — метод содержит `await`
- `Task` — асинхронная операция без значения; `Task<T>` — со значением
- По соглашению имена заканчиваются на `Async`

## HttpClient
```csharp
using var client = new HttpClient();
string html = await client.GetStringAsync("https://example.com");
Console.WriteLine(html.Length);

var response = await client.GetAsync("https://jsonplaceholder.typicode.com/users/1");
response.EnsureSuccessStatusCode();
string json = await response.Content.ReadAsStringAsync();
```

## Разбор JSON
```csharp
using System.Net.Http.Json;

record User(int Id, string Name, string Email);
var user = await client.GetFromJsonAsync<User>("https://jsonplaceholder.typicode.com/users/1");
Console.WriteLine(user?.Name);
```

## Параллельное выполнение
```csharp
var t1 = client.GetStringAsync(url1);
var t2 = client.GetStringAsync(url2);
string[] results = await Task.WhenAll(t1, t2);          // ждём оба
var first = await Task.WhenAny(t1, t2);                  // первый завершившийся
```

## Файлы
```csharp
await File.WriteAllTextAsync("a.txt", "текст");
string text = await File.ReadAllTextAsync("a.txt");
```

## Отмена
```csharp
using var cts = new CancellationTokenSource(TimeSpan.FromSeconds(3));
try
{
    await Task.Delay(10000, cts.Token);
}
catch (OperationCanceledException)
{
    Console.WriteLine("Отменено");
}
```

## Фоновые задачи
```csharp
int result = await Task.Run(() => HeavyComputation());   // счёт в другом потоке
```

## Типичные ошибки
- `.Result` или `.Wait()` вместо `await` — риск взаимной блокировки
- `async void` (допустим только для обработчиков событий)
- Не обрабатывают исключения задач
- Создают `HttpClient` на каждый запрос — переиспользуйте один экземпляр

## Практика
1. Загрузите 3 страницы параллельно и выведите их размеры.
2. Запросите список пользователей API и выведите имена.
3. Напишите метод с отменой по нажатию клавиши.

## Проверь себя
1. Что делает `await`?
2. Чем `Task` отличается от `Task<T>`?
3. Почему нельзя писать `.Result` в UI-приложении?

---
[← Урок 20](lesson-20.md) · [Программа курса](README.md) · [Урок 22 →](lesson-22.md)
