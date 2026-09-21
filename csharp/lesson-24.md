# C# · Урок 24. Итоговый проект: менеджер задач

## Цель
Консольное приложение на C# с использованием классов, интерфейсов, LINQ, JSON и обработки ошибок.

## Требования
- Добавление, просмотр, отметка выполненной, удаление задач
- Приоритеты и сроки
- Фильтры и сортировка (LINQ)
- Сохранение в `tasks.json`
- Корректная работа при неверном вводе

## Структура
```
TaskManager/
├── Program.cs
├── TaskItem.cs
├── ITaskStorage.cs
├── JsonTaskStorage.cs
├── TaskService.cs
└── TaskManager.csproj
```
Создание: `dotnet new console -n TaskManager`.

## TaskItem.cs
```csharp
public enum Priority { Low, Medium, High }

public class TaskItem
{
    public int Id { get; set; }
    public string Title { get; set; } = "";
    public bool IsDone { get; set; }
    public Priority Priority { get; set; } = Priority.Medium;
    public DateTime? Deadline { get; set; }

    public override string ToString() =>
        $"{Id,3}. [{(IsDone ? "x" : " ")}] {Title} ({Priority})" +
        (Deadline.HasValue ? $" до {Deadline:dd.MM.yyyy}" : "");
}
```

## ITaskStorage.cs и JsonTaskStorage.cs
```csharp
public interface ITaskStorage
{
    List<TaskItem> Load();
    void Save(List<TaskItem> tasks);
}
```
```csharp
using System.Text.Json;

public class JsonTaskStorage : ITaskStorage
{
    private readonly string path;
    private static readonly JsonSerializerOptions Options = new()
    {
        WriteIndented = true,
        Encoder = System.Text.Encodings.Web.JavaScriptEncoder.UnsafeRelaxedJsonEscaping
    };

    public JsonTaskStorage(string path) => this.path = path;

    public List<TaskItem> Load()
    {
        if (!File.Exists(path)) return new();
        try
        {
            return JsonSerializer.Deserialize<List<TaskItem>>(File.ReadAllText(path)) ?? new();
        }
        catch (JsonException)
        {
            Console.WriteLine("Файл данных повреждён, начинаем с пустого списка");
            return new();
        }
    }

    public void Save(List<TaskItem> tasks) =>
        File.WriteAllText(path, JsonSerializer.Serialize(tasks, Options));
}
```

## TaskService.cs
```csharp
public class TaskService
{
    private readonly ITaskStorage storage;
    private readonly List<TaskItem> tasks;

    public TaskService(ITaskStorage storage)
    {
        this.storage = storage;
        tasks = storage.Load();
    }

    public TaskItem Add(string title, Priority priority, DateTime? deadline)
    {
        if (string.IsNullOrWhiteSpace(title))
            throw new ArgumentException("Название не может быть пустым");

        var task = new TaskItem
        {
            Id = tasks.Count == 0 ? 1 : tasks.Max(t => t.Id) + 1,
            Title = title.Trim(),
            Priority = priority,
            Deadline = deadline
        };
        tasks.Add(task);
        storage.Save(tasks);
        return task;
    }

    public bool Complete(int id)
    {
        var t = tasks.FirstOrDefault(x => x.Id == id);
        if (t is null) return false;
        t.IsDone = true;
        storage.Save(tasks);
        return true;
    }

    public bool Remove(int id)
    {
        int removed = tasks.RemoveAll(x => x.Id == id);
        if (removed > 0) storage.Save(tasks);
        return removed > 0;
    }

    public IEnumerable<TaskItem> GetAll(bool onlyActive = false) =>
        tasks.Where(t => !onlyActive || !t.IsDone)
             .OrderByDescending(t => t.Priority)
             .ThenBy(t => t.Deadline ?? DateTime.MaxValue);
}
```

## Program.cs
```csharp
Console.OutputEncoding = System.Text.Encoding.UTF8;
var service = new TaskService(new JsonTaskStorage("tasks.json"));

while (true)
{
    Console.WriteLine("\n1. Все  2. Активные  3. Добавить  4. Выполнить  5. Удалить  0. Выход");
    Console.Write("> ");
    string? choice = Console.ReadLine();

    try
    {
        switch (choice)
        {
            case "1": Print(service.GetAll()); break;
            case "2": Print(service.GetAll(onlyActive: true)); break;
            case "3": AddTask(); break;
            case "4": Console.WriteLine(service.Complete(ReadInt("ID: ")) ? "Готово" : "Не найдено"); break;
            case "5": Console.WriteLine(service.Remove(ReadInt("ID: ")) ? "Удалено" : "Не найдено"); break;
            case "0": return;
            default: Console.WriteLine("Неизвестная команда"); break;
        }
    }
    catch (Exception ex)
    {
        Console.WriteLine($"Ошибка: {ex.Message}");
    }
}

void AddTask()
{
    Console.Write("Название: ");
    string title = Console.ReadLine() ?? "";
    Console.Write("Приоритет (0 - низкий, 1 - средний, 2 - высокий): ");
    var priority = Enum.TryParse<Priority>(Console.ReadLine(), out var p) ? p : Priority.Medium;
    Console.Write("Срок (дд.мм.гггг, Enter — без срока): ");
    DateTime? deadline = DateTime.TryParse(Console.ReadLine(), out var d) ? d : null;
    Console.WriteLine("Добавлено: " + service.Add(title, priority, deadline));
}

int ReadInt(string prompt)
{
    while (true)
    {
        Console.Write(prompt);
        if (int.TryParse(Console.ReadLine(), out int n)) return n;
        Console.WriteLine("Введите число");
    }
}

void Print(IEnumerable<TaskItem> items)
{
    var list = items.ToList();
    if (list.Count == 0) Console.WriteLine("Список пуст");
    list.ForEach(Console.WriteLine);
}
```

## Задания на усложнение
1. Поиск по названию, фильтр по приоритету.
2. Редактирование задачи.
3. Замените `JsonTaskStorage` на `SqliteTaskStorage` (урок 23) — класс `TaskService` менять не нужно, в этом польза интерфейса.
4. Оформите интерфейс на Windows Forms (урок 22).
5. Добавьте модульные тесты (xUnit) для `TaskService`.

## Поздравляем!
Вы прошли курс C#. Следующие шаги: ASP.NET Core (веб-API), Entity Framework Core, Unity (игры), MAUI/WPF (интерфейсы), паттерны проектирования.

---
[← Урок 23](lesson-23.md) · [Программа курса](README.md)
