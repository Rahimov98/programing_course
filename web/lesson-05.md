# Веб · Урок 5. Формы

## Цели урока
- Создавать формы и поля ввода
- Знать основные типы input
- Понимать атрибуты name, required, placeholder

## Теория

**Базовая форма**
```html
<form action="/submit" method="post">
  <label for="name">Имя:</label>
  <input type="text" id="name" name="name" required placeholder="Ваше имя">

  <label for="email">Email:</label>
  <input type="email" id="email" name="email" required>

  <label for="msg">Сообщение:</label>
  <textarea id="msg" name="message" rows="4"></textarea>

  <button type="submit">Отправить</button>
</form>
```

**Типы input**
| type | Назначение |
|------|------------|
| text | Обычный текст |
| email | Email (проверка формата) |
| password | Скрытие ввода |
| number | Число |
| date | Дата |
| checkbox | Галочка |
| radio | Выбор одного |
| file | Файл |
| submit / button / reset | Кнопки |

**Checkbox и radio**
```html
<input type="checkbox" name="agree" id="agree" value="yes">
<label for="agree">Согласен с правилами</label>

<input type="radio" name="city" value="dushanbe" id="d">
<label for="d">Душанбе</label>
<input type="radio" name="city" value="khujand" id="k">
<label for="k">Худжанд</label>
```

**Select**
```html
<select name="level">
  <option value="junior">Junior</option>
  <option value="middle" selected>Middle</option>
  <option value="senior">Senior</option>
</select>
```

**Важно**
- `label` + `for` / `id` — клик по подписи фокусирует поле
- `name` — ключ данных при отправке
- `required` — обязательное поле (браузерная проверка)

## Типичные ошибки
- Поле без `name` — данные не уйдут
- `label` без связи с полем
- `button` без `type="submit"` внутри form

## Практика
1. Форма обратной связи: имя, email, сообщение.
2. Форма регистрации: имя, email, пароль, согласие (checkbox).
3. Выбор города через radio или select.

## Проверь себя
1. Зачем атрибут `name`?
2. Чем checkbox отличается от radio?
3. Что делает `required`?

---
[← Урок 4](lesson-04.md) · [Программа курса](README.md) · [Урок 6 →](lesson-06.md)
