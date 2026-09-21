# PHP · Урок 20. Аутентификация: регистрация и вход

## Цели урока
- Регистрировать пользователей с хешированием пароля
- Проверять логин и создавать сессию
- Реализовать выход

## Теория

**Таблица users**
```sql
CREATE TABLE users (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    email VARCHAR(150) UNIQUE NOT NULL,
    password VARCHAR(255) NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

**Регистрация**
```php
$name = trim($_POST["name"] ?? "");
$email = trim($_POST["email"] ?? "");
$password = $_POST["password"] ?? "";

if (strlen($password) < 6) {
    $errors[] = "Пароль слишком короткий";
}

$hash = password_hash($password, PASSWORD_DEFAULT);

$stmt = $pdo->prepare("INSERT INTO users (name, email, password) VALUES (?, ?, ?)");
try {
    $stmt->execute([$name, $email, $hash]);
    // успех → редирект на логин
} catch (PDOException $e) {
    $errors[] = "Email уже занят";
}
```

**Вход**
```php
$email = trim($_POST["email"] ?? "");
$password = $_POST["password"] ?? "";

$stmt = $pdo->prepare("SELECT * FROM users WHERE email = ?");
$stmt->execute([$email]);
$user = $stmt->fetch();

if ($user && password_verify($password, $user["password"])) {
    session_start();
    session_regenerate_id(true);
    $_SESSION["user_id"] = $user["id"];
    $_SESSION["user_name"] = $user["name"];
    header("Location: /profile.php");
    exit;
} else {
    $errors[] = "Неверный email или пароль";
}
```

**Проверка авторизации**
```php
session_start();
if (empty($_SESSION["user_id"])) {
    header("Location: /login.php");
    exit;
}
```

**Выход**
```php
session_start();
$_SESSION = [];
session_destroy();
setcookie(session_name(), "", time() - 3600, "/");
header("Location: /");
exit;
```

## Типичные ошибки
- Хранение пароля в открытом виде
- Сравнение паролей через `==` вместо `password_verify`
- Отсутствие `session_regenerate_id` после входа

## Практика
1. Страницы `register.php` и `login.php`.
2. После входа — страница профиля с именем.
3. Кнопка «Выйти».

## Проверь себя
1. Зачем `password_hash` / `password_verify`?
2. Почему нельзя хранить пароль как есть?
3. Зачем `session_regenerate_id` при входе?

---
[← Урок 19](lesson-19.md) · [Программа курса](README.md) · [Урок 21 →](lesson-21.md)
