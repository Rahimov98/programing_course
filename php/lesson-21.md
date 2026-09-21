# PHP · Урок 21. Безопасность: XSS, CSRF, SQL-инъекции

## Цели урока
- Понимать основные веб-уязвимости
- Защищаться от XSS, CSRF и SQL-инъекций
- Применять безопасные практики

## Теория

**1. SQL-инъекции**
Уже защищены подготовленными запросами (урок 19). Никогда не вставляйте пользовательский ввод напрямую в SQL.

**2. XSS (Cross-Site Scripting)**
Вредоносный JS через пользовательский ввод.

```php
// ПЛОХО
echo $_GET["name"];

// ХОРОШО
echo htmlspecialchars($_GET["name"] ?? "", ENT_QUOTES, "UTF-8");
```

В шаблонах всегда экранируйте вывод. Для HTML-атрибутов — тоже `htmlspecialchars`.

**3. CSRF (Cross-Site Request Forgery)**
Поддельный запрос от имени залогиненного пользователя.

Защита — токен:
```php
// при генерации формы
session_start();
$_SESSION["csrf_token"] = bin2hex(random_bytes(32));
```
```html
<input type="hidden" name="csrf_token" value="<?= $_SESSION["csrf_token"] ?>">
```
```php
// при обработке
if (!hash_equals($_SESSION["csrf_token"] ?? "", $_POST["csrf_token"] ?? "")) {
    die("Неверный CSRF-токен");
}
```

**Дополнительные меры**
- `password_hash` / `password_verify`
- HTTPS
- `httponly` и `secure` для cookies
- Ограничение загружаемых файлов (тип, размер)
- Минимальные права БД (не root)
- Заголовки: `X-Content-Type-Options`, `X-Frame-Options`, `Content-Security-Policy`

## Типичные ошибки
- Экранирование только «иногда»
- CSRF-токен не проверяется на всех POST-формах
- Отключение проверки SSL в cURL

## Практика
1. Во всех выводах пользовательских данных добавьте `htmlspecialchars`.
2. Добавьте CSRF-токен в форму логина/регистрации.
3. Убедитесь, что все SQL-запросы используют `prepare`.

## Проверь себя
1. Что такое XSS и как от него защититься?
2. Зачем CSRF-токен?
3. Почему `hash_equals` лучше `===` для токенов?

---
[← Урок 20](lesson-20.md) · [Программа курса](README.md) · [Урок 22 →](lesson-22.md)
