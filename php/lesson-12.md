# PHP · Урок 12. Загрузка файлов

## Цели урока
- Принимать файлы через форму
- Проверять тип, размер и ошибки загрузки
- Сохранять файлы безопасно

## Теория

**Форма** (обязательно `enctype`)
```html
<form action="upload.php" method="post" enctype="multipart/form-data">
  <input type="file" name="avatar" accept="image/*">
  <button type="submit">Загрузить</button>
</form>
```

**Обработка**
```php
<?php
if ($_SERVER["REQUEST_METHOD"] === "POST" && isset($_FILES["avatar"])) {
    $file = $_FILES["avatar"];

    if ($file["error"] !== UPLOAD_ERR_OK) {
        die("Ошибка загрузки: " . $file["error"]);
    }

    // проверки
    $maxSize = 2 * 1024 * 1024; // 2 МБ
    if ($file["size"] > $maxSize) {
        die("Файл слишком большой");
    }

    $allowed = ["image/jpeg", "image/png", "image/gif"];
    $finfo = finfo_open(FILEINFO_MIME_TYPE);
    $mime = finfo_file($finfo, $file["tmp_name"]);
    finfo_close($finfo);

    if (!in_array($mime, $allowed)) {
        die("Недопустимый тип файла");
    }

    // безопасное имя
    $ext = pathinfo($file["name"], PATHINFO_EXTENSION);
    $newName = uniqid("img_", true) . "." . strtolower($ext);
    $dest = __DIR__ . "/uploads/" . $newName;

    if (!is_dir(__DIR__ . "/uploads")) {
        mkdir(__DIR__ . "/uploads", 0755, true);
    }

    if (move_uploaded_file($file["tmp_name"], $dest)) {
        echo "Файл сохранён: $newName";
    } else {
        echo "Не удалось сохранить";
    }
}
```

**$_FILES["avatar"] содержит:**
- `name` — оригинальное имя
- `type` — MIME (ненадёжен)
- `tmp_name` — временный путь
- `error` — код ошибки
- `size` — размер в байтах

## Типичные ошибки
- Забыли `enctype="multipart/form-data"`
- Доверились `$_FILES["type"]` вместо `finfo`
- Сохранили файл с оригинальным именем (риск перезаписи и path traversal)
- Папка `uploads` недоступна для записи

## Практика
1. Сделайте форму загрузки изображения.
2. Проверьте размер (макс. 1 МБ) и тип (только JPEG/PNG).
3. Сохраните файл со случайным именем в папку `uploads/`.

## Проверь себя
1. Зачем `move_uploaded_file` вместо `rename`?
2. Почему нельзя доверять расширению из имени файла?
3. Что такое `UPLOAD_ERR_INI_SIZE`?

---
[← Урок 11](lesson-11.md) · [Программа курса](README.md) · [Урок 13 →](lesson-13.md)
