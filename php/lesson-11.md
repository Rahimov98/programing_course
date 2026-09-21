# PHP · Урок 11. Работа с файлами

## Цели урока
- Читать и записывать файлы
- Проверять существование и права
- Работать с CSV и простым логированием

## Теория

**Чтение**
```php
$content = file_get_contents("data.txt");
$lines = file("data.txt", FILE_IGNORE_NEW_LINES);
```

**Запись**
```php
file_put_contents("log.txt", "Новая запись\n", FILE_APPEND);
// или перезапись:
file_put_contents("data.txt", "Полный текст");
```

**Проверки**
```php
if (file_exists("data.txt")) {
    echo filesize("data.txt");  // размер в байтах
}
is_readable("data.txt");
is_writable("data.txt");
```

**Открытие потока**
```php
$fp = fopen("data.txt", "r");  // r, w, a, r+, ...
if ($fp) {
    while (($line = fgets($fp)) !== false) {
        echo $line;
    }
    fclose($fp);
}
```

**CSV**
```php
$fp = fopen("users.csv", "r");
while (($row = fgetcsv($fp, 0, ",")) !== false) {
    // $row — массив колонок
}
fclose($fp);

// запись
$fp = fopen("users.csv", "a");
fputcsv($fp, ["Алишер", "ali@example.com"]);
fclose($fp);
```

**Удаление и переименование**
```php
unlink("old.txt");
rename("a.txt", "b.txt");
```

## Типичные ошибки
- Забыли проверить существование файла
- Права доступа (на хостинге папка должна быть writable)
- Не закрыли `fclose` при работе с большими файлами
- Путь относительно текущего скрипта — используйте `__DIR__`

## Практика
1. Запишите текущую дату и время в `log.txt` (добавление).
2. Прочитайте файл и выведите построчно.
3. Создайте CSV с тремя пользователями и выведите его содержимое.

## Проверь себя
1. Чем `file_get_contents` отличается от `fopen`?
2. Что делает флаг `FILE_APPEND`?
3. Зачем `__DIR__`?

---
[← Урок 10](lesson-10.md) · [Программа курса](README.md) · [Урок 12 →](lesson-12.md)
