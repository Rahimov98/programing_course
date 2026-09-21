# C# · Урок 18. Работа с файлами

## Цели урока
- Читать и записывать текст и JSON
- Работать с путями и папками

## Быстрые методы `File`
```csharp
File.WriteAllText("notes.txt", "Первая строка\n");
File.AppendAllText("notes.txt", "Вторая строка\n");
string text = File.ReadAllText("notes.txt");
string[] lines = File.ReadAllLines("notes.txt");
File.WriteAllLines("out.txt", new[] { "a", "b" });
bool exists = File.Exists("notes.txt");
File.Copy("a.txt", "b.txt", overwrite: true);
File.Delete("b.txt");
```
Для больших файлов читайте построчно: `foreach (var line in File.ReadLines("big.txt"))`.

## StreamReader / StreamWriter
```csharp
using (var writer = new StreamWriter("log.txt", append: true))
{
    writer.WriteLine($"{DateTime.Now}: запуск");
}

using var reader = new StreamReader("log.txt");
string? line;
while ((line = reader.ReadLine()) != null)
    Console.WriteLine(line);
```

## Пути и папки
```csharp
string path = Path.Combine("data", "students", "list.txt");
Path.GetFileName(path);            // list.txt
Path.GetExtension(path);           // .txt
Directory.CreateDirectory("data");
Directory.Exists("data");
foreach (var f in Directory.GetFiles("data", "*.txt")) Console.WriteLine(f);
```

## JSON
```csharp
using System.Text.Json;

record Student(string Name, int Age, double Gpa);

var students = new List<Student> { new("Али", 21, 4.5), new("Мадина", 19, 4.8) };

var options = new JsonSerializerOptions
{
    WriteIndented = true,
    Encoder = System.Text.Encodings.Web.JavaScriptEncoder.UnsafeRelaxedJsonEscaping   // кириллица без \uXXXX
};

string json = JsonSerializer.Serialize(students, options);
File.WriteAllText("students.json", json);

var loaded = JsonSerializer.Deserialize<List<Student>>(File.ReadAllText("students.json"));
```

## CSV вручную
```csharp
foreach (var line in File.ReadLines("data.csv").Skip(1))
{
    var parts = line.Split(';');
    Console.WriteLine($"{parts[0]} — {parts[1]}");
}
```

## Типичные ошибки
- Относительный путь считается от папки запуска (`bin/Debug/...`), а не от папки проекта
- Забыли `using` — файл остаётся заблокированным
- `ReadAllText` для огромных файлов расходует много памяти
- Пути с `\` — используйте `Path.Combine`

## Практика
1. Запишите 10 случайных чисел в файл и прочитайте обратно.
2. Посчитайте строки и слова в текстовом файле.
3. Сохраните список студентов в JSON и загрузите при запуске.

## Проверь себя
1. Чем `File.ReadAllText` отличается от `StreamReader`?
2. Зачем нужен `using`?
3. Как сохранить объект в JSON?

---
[← Урок 17](lesson-17.md) · [Программа курса](README.md) · [Урок 19 →](lesson-19.md)
