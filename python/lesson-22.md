# Python · Урок 22. Библиотека requests и работа с API

## Цели урока
- Отправлять HTTP-запросы
- Получать и разбирать JSON из API

## Установка
```bash
pip install requests
```

## GET-запрос
```python
import requests

r = requests.get("https://api.github.com/users/octocat", timeout=10)
print(r.status_code)     # 200
data = r.json()
print(data["name"], data["public_repos"])
```

## Параметры и заголовки
```python
r = requests.get(
    "https://httpbin.org/get",
    params={"q": "python", "page": 2},
    headers={"User-Agent": "my-app/1.0"},
    timeout=10,
)
print(r.url)
```

## POST-запрос
```python
r = requests.post("https://httpbin.org/post", json={"name": "Алишер"}, timeout=10)
print(r.json())
```

## Обработка ошибок
```python
try:
    r = requests.get("https://example.com/api", timeout=5)
    r.raise_for_status()          # исключение при 4xx/5xx
except requests.exceptions.RequestException as e:
    print("Ошибка запроса:", e)
```

## Коды ответов
`200` OK · `201` создано · `400` неверный запрос · `401/403` нет доступа · `404` не найдено · `500` ошибка сервера.

## Типичные ошибки
- Нет `timeout` — программа может зависнуть
- Не проверяют `status_code` перед `.json()`
- Ключи API в коде, который выкладывают на GitHub — храните их в переменных окружения

## Практика
1. Получите информацию о пользователе GitHub и выведите число репозиториев.
2. Скачайте курс валют из открытого API и выведите таблицу.
3. Сохраните ответ API в файл JSON.

## Проверь себя
1. Что означает код 404?
2. Зачем нужен `timeout`?
3. Как передать параметры запроса?

---
[← Урок 21](lesson-21.md) · [Программа курса](README.md) · [Урок 23 →](lesson-23.md)
