# PHP · Урок 23. Основы MVC

## Цели урока
- Понять паттерн Model-View-Controller
- Разделить код на слои
- Сделать простой роутинг

## Теория

**MVC**
- **Model** — данные и бизнес-логика (работа с БД)
- **View** — отображение (HTML-шаблоны)
- **Controller** — принимает запрос, вызывает Model, передаёт данные во View

**Структура**
```
project/
├── public/
│   └── index.php          # единая точка входа
├── app/
│   ├── Controllers/
│   │   └── UserController.php
│   ├── Models/
│   │   └── User.php
│   └── Views/
│       ├── layout.php
│       └── users/
│           └── index.php
├── config/
│   └── database.php
└── routes.php
```

**index.php (фронт-контроллер)**
```php
<?php
require __DIR__ . "/../vendor/autoload.php"; // или своя автозагрузка
require __DIR__ . "/../config/database.php";
require __DIR__ . "/../routes.php";

$uri = parse_url($_SERVER["REQUEST_URI"], PHP_URL_PATH);
$method = $_SERVER["REQUEST_METHOD"];

if (isset($routes[$method][$uri])) {
    [$controller, $action] = $routes[$method][$uri];
    (new $controller($pdo))->$action();
} else {
    http_response_code(404);
    echo "Страница не найдена";
}
```

**routes.php**
```php
$routes = [
    "GET" => [
        "/users" => [UserController::class, "index"],
        "/users/create" => [UserController::class, "create"],
    ],
    "POST" => [
        "/users" => [UserController::class, "store"],
    ],
];
```

**Model (упрощённо)**
```php
class User {
    public function __construct(private PDO $pdo) {}

    public function all(): array {
        return $this->pdo->query("SELECT * FROM users")->fetchAll();
    }
}
```

**Controller**
```php
class UserController {
    public function __construct(private PDO $pdo) {}

    public function index(): void {
        $users = (new User($this->pdo))->all();
        require __DIR__ . "/../Views/users/index.php";
    }
}
```

**View**
```php
<?php require __DIR__ . "/../layout.php"; ?>
<h1>Пользователи</h1>
<ul>
<?php foreach ($users as $u): ?>
  <li><?= htmlspecialchars($u["name"]) ?></li>
<?php endforeach; ?>
</ul>
```

## Типичные ошибки
- Бизнес-логика прямо в View
- SQL-запросы в Controller
- Множество точек входа вместо одного `index.php`

## Практика
1. Сделайте список пользователей через Controller + Model + View.
2. Добавьте маршрут и действие для создания пользователя.
3. Вынесите общий layout (header/footer).

## Проверь себя
1. Какие обязанности у Model, View и Controller?
2. Зачем единая точка входа?
3. Что такое роутинг?

---
[← Урок 22](lesson-22.md) · [Программа курса](README.md) · [Урок 24 →](lesson-24.md)
