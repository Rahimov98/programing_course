# PHP · Урок 17. Подключение файлов и структура проекта

## Цели урока
- Подключать файлы через `require` / `include`
- Организовать простую структуру проекта
- Использовать автозагрузку классов

## Теория

**Подключение**
```php
require "config.php";          // обязательный файл
require_once "config.php";     // только один раз
include "header.php";          // не критичный
include_once "header.php";
```

Разница: `require` при ошибке — Fatal error, `include` — Warning.

**Структура проекта**
```
project/
├── public/
│   └── index.php          # точка входа
├── src/
│   ├── Config.php
│   ├── User.php
│   └── helpers.php
├── templates/
│   ├── header.php
│   └── footer.php
├── vendor/                # Composer
└── composer.json
```

**Пример index.php**
```php
<?php
require_once __DIR__ . "/../src/helpers.php";
require_once __DIR__ . "/../src/User.php";

$user = new User("Алишер");
include __DIR__ . "/../templates/header.php";
echo $user->greet();
include __DIR__ . "/../templates/footer.php";
```

**Автозагрузка (простая)**
```php
spl_autoload_register(function ($class) {
    $file = __DIR__ . "/src/" . $class . ".php";
    if (file_exists($file)) {
        require $file;
    }
});
```

**Composer (рекомендуется)**
```json
{
  "autoload": {
    "psr-4": {
      "App\\": "src/"
    }
  }
}
```
Затем `composer dump-autoload` и `require "vendor/autoload.php";`.

## Типичные ошибки
- Относительные пути без `__DIR__`
- Циклические подключения
- Подключение одного и того же файла много раз без `_once`

## Практика
1. Создайте `config.php` с константами сайта.
2. Разделите страницу на `header.php`, `content.php`, `footer.php`.
3. Напишите простую автозагрузку для класса `User`.

## Проверь себя
1. Чем `require` отличается от `include`?
2. Зачем `require_once`?
3. Что такое PSR-4?

---
[← Урок 16](lesson-16.md) · [Программа курса](README.md) · [Урок 18 →](lesson-18.md)
