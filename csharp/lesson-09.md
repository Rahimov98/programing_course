# C# · Урок 9. Строки

## Цели урока
- Использовать методы `string` и `StringBuilder`

## Основы
```csharp
string s = "Привет, мир";
Console.WriteLine(s.Length);         // 11
Console.WriteLine(s[0]);             // П
string t = s + "!";
```
Строки **неизменяемы**: методы возвращают новую строку.

## Методы
```csharp
string text = "  Hello, World  ";
text.Trim();  text.TrimStart();  text.TrimEnd();
text.ToUpper();  text.ToLower();
text.Contains("World");
text.StartsWith("He");  text.EndsWith("ld");
text.IndexOf("World");             // -1, если нет
text.Substring(2, 5);              // 5 символов с индекса 2
text.Replace("World", "C#");
"a,b,c".Split(',');                // string[]
string.Join(", ", new[] { "a", "b" });
"5".PadLeft(3, '0');               // 005
string.IsNullOrEmpty(text);
string.IsNullOrWhiteSpace(text);
```

## Сравнение
```csharp
"abc" == "abc";                                   // true
string.Equals("A", "a", StringComparison.OrdinalIgnoreCase);
"apple".CompareTo("banana");                      // < 0
```

## Полезные приёмы
```csharp
// разворот
string rev = new string("привет".Reverse().ToArray());

// подсчёт слов
int words = "раз два три".Split(' ', StringSplitOptions.RemoveEmptyEntries).Length;

// многострочная и «сырая» строка
string path = @"C:\Users\Ali";
string json = """{ "name": "Али" }""";
```

## StringBuilder
При множестве конкатенаций в цикле используйте `StringBuilder`:
```csharp
using System.Text;

var sb = new StringBuilder();
for (int i = 0; i < 1000; i++) sb.Append(i).Append(',');
string result = sb.ToString();
```

## Символы
```csharp
char.IsDigit('5'); char.IsLetter('a'); char.IsUpper('A');
char.ToUpper('a');
```

## Типичные ошибки
- Конкатенация в цикле создаёт много временных строк — берите `StringBuilder`
- `s.Replace(...)` без присваивания результата
- Сравнение строк через `==` без учёта регистра — результат может удивить

## Практика
1. Проверьте, является ли строка палиндромом.
2. Подсчитайте гласные и согласные.
3. Сделайте первую букву каждого слова заглавной.

## Проверь себя
1. Почему строки называют неизменяемыми?
2. Когда нужен `StringBuilder`?
3. Как разделить строку на слова?

---
[← Урок 8](lesson-08.md) · [Программа курса](README.md) · [Урок 10 →](lesson-10.md)
