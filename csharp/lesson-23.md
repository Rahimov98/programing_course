# C# · Урок 23. Работа с базой данных (SQLite)

## Цели урока
- Подключаться к SQLite
- Выполнять безопасные параметризованные запросы

## Установка пакета
```bash
dotnet add package Microsoft.Data.Sqlite
```

## Подключение и создание таблицы
```csharp
using Microsoft.Data.Sqlite;

using var connection = new SqliteConnection("Data Source=app.db");
connection.Open();

var create = connection.CreateCommand();
create.CommandText = """
    CREATE TABLE IF NOT EXISTS students (
        id   INTEGER PRIMARY KEY AUTOINCREMENT,
        name TEXT NOT NULL,
        age  INTEGER
    )
    """;
create.ExecuteNonQuery();
```

## Добавление данных
Всегда используйте **параметры**, никогда не склеивайте SQL из строк — это защита от SQL-инъекций:
```csharp
var insert = connection.CreateCommand();
insert.CommandText = "INSERT INTO students (name, age) VALUES ($name, $age)";
insert.Parameters.AddWithValue("$name", "Алишер");
insert.Parameters.AddWithValue("$age", 21);
insert.ExecuteNonQuery();
```

## Чтение
```csharp
var select = connection.CreateCommand();
select.CommandText = "SELECT id, name, age FROM students WHERE age >= $min ORDER BY name";
select.Parameters.AddWithValue("$min", 18);

using var reader = select.ExecuteReader();
while (reader.Read())
{
    int id = reader.GetInt32(0);
    string name = reader.GetString(1);
    int age = reader.IsDBNull(2) ? 0 : reader.GetInt32(2);
    Console.WriteLine($"{id}: {name}, {age}");
}
```

## Скалярные значения
```csharp
var count = connection.CreateCommand();
count.CommandText = "SELECT COUNT(*) FROM students";
long total = (long)count.ExecuteScalar()!;
```

## Обновление и удаление
```csharp
var update = connection.CreateCommand();
update.CommandText = "UPDATE students SET age = $age WHERE id = $id";
update.Parameters.AddWithValue("$age", 22);
update.Parameters.AddWithValue("$id", 1);
int rows = update.ExecuteNonQuery();     // число изменённых строк
```

## Транзакции
```csharp
using var tx = connection.BeginTransaction();
try
{
    // несколько команд ...
    tx.Commit();
}
catch
{
    tx.Rollback();
    throw;
}
```

## Репозиторий
```csharp
class StudentRepository
{
    private readonly string connString;
    public StudentRepository(string dbPath) => connString = $"Data Source={dbPath}";

    public List<Student> GetAll()
    {
        var list = new List<Student>();
        using var c = new SqliteConnection(connString);
        c.Open();
        var cmd = c.CreateCommand();
        cmd.CommandText = "SELECT id, name, age FROM students";
        using var r = cmd.ExecuteReader();
        while (r.Read()) list.Add(new Student(r.GetInt32(0), r.GetString(1), r.GetInt32(2)));
        return list;
    }
}
record Student(int Id, string Name, int Age);
```

## Дальше
Для больших проектов используют ORM **Entity Framework Core**: работа с таблицами через классы и LINQ.

## Типичные ошибки
- SQL из конкатенации строк → SQL-инъекция
- Не освободили соединение (забыли `using`)
- Не обработали `NULL` (`IsDBNull`)
- Относительный путь к файлу базы зависит от рабочей папки

## Практика
1. Создайте таблицу `books` и реализуйте добавление, вывод и удаление.
2. Найдите книги по части названия (`LIKE`).
3. Добавьте транзакцию для пакетного добавления.

## Проверь себя
1. Зачем нужны параметры в SQL-запросах?
2. Чем `ExecuteNonQuery` отличается от `ExecuteScalar`?
3. Что такое транзакция?

---
[← Урок 22](lesson-22.md) · [Программа курса](README.md) · [Урок 24 →](lesson-24.md)
