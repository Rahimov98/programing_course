# C# · Урок 7. Методы

## Цели урока
- Выносить код в методы
- Понимать параметры `ref`, `out`, необязательные и именованные

## Определение
```csharp
static int Square(int x) => x * x;

static void Greet(string name)
{
    Console.WriteLine($"Привет, {name}!");
}

static double Average(int a, int b)
{
    return (a + b) / 2.0;
}

Greet("Мадина");
Console.WriteLine(Square(5));
```
`void` — метод ничего не возвращает. В top-level программе методы можно объявлять в любом месте файла.

## Необязательные и именованные параметры
```csharp
static double Power(double b, int exp = 2)
{
    double r = 1;
    for (int i = 0; i < exp; i++) r *= b;
    return r;
}

Power(3);              // 9
Power(2, 10);          // 1024
Power(exp: 3, b: 2);   // 8
```

## Перегрузка
```csharp
static int Max(int a, int b) => a > b ? a : b;
static double Max(double a, double b) => a > b ? a : b;
```

## out и ref
```csharp
static bool TryDivide(int a, int b, out int result)
{
    if (b == 0) { result = 0; return false; }
    result = a / b;
    return true;
}
if (TryDivide(10, 2, out int r)) Console.WriteLine(r);

static void Swap(ref int a, ref int b)
{
    (a, b) = (b, a);
}
int x = 1, y = 2;
Swap(ref x, ref y);       // x=2, y=1
```

## Кортежи для нескольких значений
```csharp
static (int min, int max) MinMax(int[] arr) => (arr.Min(), arr.Max());
var (lo, hi) = MinMax(new[] { 3, 1, 8 });
```

## params
```csharp
static int Sum(params int[] nums) => nums.Sum();
Sum(1, 2, 3, 4);
```

## Рекурсия
```csharp
static long Factorial(int n) => n <= 1 ? 1 : n * Factorial(n - 1);
```

## Типичные ошибки
- Забыли `return` в методе с возвращаемым типом
- Не присвоили `out` параметр во всех ветках
- Рекурсия без базового случая → `StackOverflow`

## Практика
1. `IsPrime(int n)`.
2. `Gcd(int a, int b)`.
3. Метод, возвращающий кортеж (среднее, сумма) для массива.

## Проверь себя
1. Чем `ref` отличается от `out`?
2. Что такое перегрузка методов?
3. Для чего нужен `params`?

---
[← Урок 6](lesson-06.md) · [Программа курса](README.md) · [Урок 8 →](lesson-08.md)
