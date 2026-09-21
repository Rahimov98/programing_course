# C# · Урок 2. Переменные и типы данных

## Цели урока
- Объявлять переменные и константы
- Знать основные типы и преобразования

## Объявление
```csharp
int age = 21;
double price = 19.99;
decimal money = 1500.50m;      // для денег: точные вычисления
char grade = 'A';
string name = "Алишер";
bool isStudent = true;
const double Pi = 3.14159;

var city = "Душанбе";          // тип определяется по значению (string)

Console.WriteLine($"{name}, {age} лет, {city}");
```
C# — язык со **строгой статической типизацией**: тип переменной задаётся один раз.

## Основные типы
| Тип | Размер | Значение |
|---|---|---|
| `byte` | 1 байт | 0…255 |
| `short` | 2 байта | ±32 тыс. |
| `int` | 4 байта | ±2,1 млрд |
| `long` | 8 байт | очень большие целые |
| `float` | 4 байта | дробное (суффикс `f`) |
| `double` | 8 байт | дробное |
| `decimal` | 16 байт | деньги (суффикс `m`) |
| `char` | 2 байта | символ |
| `bool` | 1 байт | `true`/`false` |
| `string` | — | строка |

Границы типов: `int.MaxValue`, `int.MinValue`.

## Преобразование типов
```csharp
int a = 10;
double b = a;                    // неявное (без потерь)
double c = 7.9;
int d = (int)c;                  // явное: 7, дробная часть отбрасывается

int n = int.Parse("123");
bool ok = int.TryParse("abc", out int result);   // false, безопасно
string s = 42.ToString();
int x = Convert.ToInt32("15");
```

## Nullable
```csharp
int? maybe = null;
if (maybe.HasValue) Console.WriteLine(maybe.Value);
int value = maybe ?? 0;          // значение по умолчанию
```

## Типичные ошибки
- `int / int` даёт целое: `7 / 2 == 3`
- `float f = 3.5;` — ошибка, нужен `3.5f`
- `int.Parse("abc")` бросает исключение — используйте `TryParse`
- Переполнение `int` без предупреждения (включить проверку: `checked`)

## Практика
1. Объявите переменные разных типов и выведите их.
2. Найдите `long.MaxValue` и `byte.MaxValue`.
3. Преобразуйте строку `"3.14"` в `double` через `TryParse`.

## Проверь себя
1. Чем `double` отличается от `decimal`?
2. Что делает `var`?
3. Зачем `TryParse`?

---
[← Урок 1](lesson-01.md) · [Программа курса](README.md) · [Урок 3 →](lesson-03.md)
