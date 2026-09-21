# PHP · Урок 22. JSON и API

## Цели урока
- Кодировать и декодировать JSON
- Создавать простой REST-подобный API
- Отправлять JSON-ответы и принимать JSON-тело

## Теория

**JSON в PHP**
```php
$data = ["name" => "Мадина", "age" => 21];
$json = json_encode($data, JSON_UNESCAPED_UNICODE);
// {"name":"Мадина","age":21}

$arr = json_decode($json, true);  // ассоциативный массив
$obj = json_decode($json);        // объект stdClass
```

**Простой API (api/users.php)**
```php
<?php
header("Content-Type: application/json; charset=utf-8");
header("Access-Control-Allow-Origin: *"); // для разработки

require __DIR__ . "/../config/db.php";

$method = $_SERVER["REQUEST_METHOD"];

if ($method === "GET") {
    $stmt = $pdo->query("SELECT id, name, email FROM users");
    echo json_encode($stmt->fetchAll(), JSON_UNESCAPED_UNICODE);
    exit;
}

if ($method === "POST") {
    $input = json_decode(file_get_contents("php://input"), true);
    if (!$input || empty($input["name"]) || empty($input["email"])) {
        http_response_code(400);
        echo json_encode(["error" => "Неверные данные"]);
        exit;
    }
    $stmt = $pdo->prepare("INSERT INTO users (name, email) VALUES (?, ?)");
    $stmt->execute([$input["name"], $input["email"]]);
    http_response_code(201);
    echo json_encode(["id" => $pdo->lastInsertId()]);
    exit;
}

http_response_code(405);
echo json_encode(["error" => "Метод не поддерживается"]);
```

**Клиент (fetch в JS)**
```javascript
fetch("/api/users.php")
  .then(r => r.json())
  .then(data => console.log(data));
```

**Коды ответа**
- 200 OK
- 201 Created
- 400 Bad Request
- 401 Unauthorized
- 404 Not Found
- 405 Method Not Allowed
- 500 Internal Server Error

## Типичные ошибки
- Забыли заголовок `Content-Type: application/json`
- `json_encode` без `JSON_UNESCAPED_UNICODE` (кириллица превращается в \uXXXX)
- Не обработали `json_last_error()`

## Практика
1. API, возвращающий список пользователей в JSON.
2. POST-эндпоинт, принимающий JSON и создающий запись.
3. Обработайте ошибку неверного JSON (код 400).

## Проверь себя
1. Чем `json_decode($s, true)` отличается от `json_decode($s)`?
2. Зачем `file_get_contents("php://input")`?
3. Какой код ответа при успешном создании ресурса?

---
[← Урок 21](lesson-21.md) · [Программа курса](README.md) · [Урок 23 →](lesson-23.md)
