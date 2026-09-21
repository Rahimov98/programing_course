# PHP · Урок 10. Валидация данных формы

## Цели урока
- Проверять обязательные поля
- Фильтровать и очищать ввод
- Показывать ошибки пользователю

## Теория

**Базовая проверка**
```php
$errors = [];

$name = trim($_POST["name"] ?? "");
$email = trim($_POST["email"] ?? "");

if ($name === "") {
    $errors[] = "Имя обязательно";
}
if ($email === "" || !filter_var($email, FILTER_VALIDATE_EMAIL)) {
    $errors[] = "Некорректный email";
}

if (empty($errors)) {
    // данные корректны
    echo "OK: $name, $email";
} else {
    foreach ($errors as $e) {
        echo "<p style='color:red'>$e</p>";
    }
}
```

**Фильтры PHP**
```php
$email = filter_input(INPUT_POST, "email", FILTER_VALIDATE_EMAIL);
$age   = filter_input(INPUT_POST, "age", FILTER_VALIDATE_INT, [
    "options" => ["min_range" => 1, "max_range" => 120]
]);
$url   = filter_input(INPUT_POST, "site", FILTER_VALIDATE_URL);
```

**Очистка (sanitize)**
```php
$safe = htmlspecialchars($name, ENT_QUOTES, "UTF-8");
// или
$safe = filter_var($name, FILTER_SANITIZE_SPECIAL_CHARS);
```

**Длина и регулярки**
```php
if (mb_strlen($name) < 2) {
    $errors[] = "Имя слишком короткое";
}
if (!preg_match("/^[a-zA-Zа-яА-ЯёЁ\s-]+$/u", $name)) {
    $errors[] = "Имя содержит недопустимые символы";
}
```

## Типичные ошибки
- Валидация только на клиенте (JS) — её легко обойти
- Вывод ошибок без экранирования
- `empty("0")` возвращает `true`

## Практика
1. Форма регистрации: имя, email, пароль (мин. 6 символов).
2. Выведите список ошибок, если есть.
3. При успехе покажите «Регистрация прошла успешно» (без сохранения пока).

## Проверь себя
1. Зачем нужна серверная валидация?
2. Что делает `htmlspecialchars`?
3. Чем `FILTER_VALIDATE_EMAIL` отличается от `FILTER_SANITIZE_EMAIL`?

---
[← Урок 9](lesson-09.md) · [Программа курса](README.md) · [Урок 11 →](lesson-11.md)
