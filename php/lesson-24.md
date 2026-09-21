# PHP · Урок 24. Итоговый проект: мини-блог

## Цель
Собрать рабочий мини-блог с регистрацией, созданием и просмотром постов, используя всё изученное: формы, сессии, PDO, ООП, безопасность.

## Требования
- Регистрация и вход (пароли через `password_hash`)
- Создание, просмотр и удаление своих постов
- Список всех постов на главной
- Защита от XSS и CSRF
- Простая структура (можно без полного MVC)

## Структура
```
blog/
├── public/
│   ├── index.php
│   ├── login.php
│   ├── register.php
│   ├── logout.php
│   ├── post.php
│   ├── create.php
│   └── delete.php
├── src/
│   ├── db.php
│   ├── auth.php
│   └── helpers.php
├── templates/
│   ├── header.php
│   └── footer.php
└── sql/
    └── schema.sql
```

## schema.sql
```sql
CREATE DATABASE blog CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
USE blog;

CREATE TABLE users (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    email VARCHAR(150) UNIQUE NOT NULL,
    password VARCHAR(255) NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE posts (
    id INT AUTO_INCREMENT PRIMARY KEY,
    user_id INT NOT NULL,
    title VARCHAR(200) NOT NULL,
    body TEXT NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (user_id) REFERENCES users(id) ON DELETE CASCADE
);
```

## db.php
```php
<?php
$pdo = new PDO(
    "mysql:host=localhost;dbname=blog;charset=utf8mb4",
    "root",
    "",
    [
        PDO::ATTR_ERRMODE => PDO::ERRMODE_EXCEPTION,
        PDO::ATTR_DEFAULT_FETCH_MODE => PDO::FETCH_ASSOC,
    ]
);
```

## helpers.php
```php
<?php
function e(?string $s): string {
    return htmlspecialchars($s ?? "", ENT_QUOTES, "UTF-8");
}

function redirect(string $url): never {
    header("Location: $url");
    exit;
}

function csrf_token(): string {
    if (empty($_SESSION["csrf"])) {
        $_SESSION["csrf"] = bin2hex(random_bytes(32));
    }
    return $_SESSION["csrf"];
}

function csrf_field(): string {
    return '<input type="hidden" name="csrf" value="' . e(csrf_token()) . '">';
}

function check_csrf(): void {
    if (!hash_equals($_SESSION["csrf"] ?? "", $_POST["csrf"] ?? "")) {
        die("CSRF token mismatch");
    }
}
```

## auth.php
```php
<?php
session_start();
require __DIR__ . "/db.php";
require __DIR__ . "/helpers.php";

function current_user(): ?array {
    if (empty($_SESSION["user_id"])) return null;
    global $pdo;
    $stmt = $pdo->prepare("SELECT id, name, email FROM users WHERE id = ?");
    $stmt->execute([$_SESSION["user_id"]]);
    return $stmt->fetch() ?: null;
}

function require_login(): array {
    $user = current_user();
    if (!$user) redirect("/login.php");
    return $user;
}
```

## Главная (index.php) — список постов
```php
<?php
require __DIR__ . "/../src/auth.php";
$posts = $pdo->query(
    "SELECT p.*, u.name AS author FROM posts p JOIN users u ON u.id = p.user_id ORDER BY p.created_at DESC"
)->fetchAll();
require __DIR__ . "/../templates/header.php";
?>
<h1>Мини-блог</h1>
<?php if (current_user()): ?>
  <p><a href="/create.php">Новый пост</a> | <a href="/logout.php">Выйти</a></p>
<?php else: ?>
  <p><a href="/login.php">Войти</a> | <a href="/register.php">Регистрация</a></p>
<?php endif; ?>

<?php foreach ($posts as $p): ?>
  <article>
    <h2><a href="/post.php?id=<?= (int)$p["id"] ?>"><?= e($p["title"]) ?></a></h2>
    <p><?= e(mb_substr($p["body"], 0, 150)) ?>...</p>
    <small><?= e($p["author"]) ?> · <?= e($p["created_at"]) ?></small>
  </article>
<?php endforeach; ?>
<?php require __DIR__ . "/../templates/footer.php"; ?>
```

## create.php (создание поста)
- Только для авторизованных
- CSRF-токен
- Валидация title и body
- INSERT через prepare

## post.php
- Показать один пост по `id`
- Если автор — кнопка «Удалить»

## delete.php
- POST + CSRF
- Проверка, что пост принадлежит текущему пользователю
- DELETE

## Что должно получиться
1. Гость видит список постов и может зарегистрироваться/войти.
2. Пользователь создаёт посты, видит свои и чужие.
3. Удаляет только свои.
4. Все выводы экранированы, формы защищены CSRF, пароли хешированы.

## Дополнительно (по желанию)
- Пагинация
- Редактирование постов
- Загрузка картинки к посту
- Простой поиск

**Поздравляем!** Вы прошли курс PHP с нуля до рабочего веб-приложения.

---
[← Урок 23](lesson-23.md) · [Программа курса](README.md)
