# JavaScript · Урок 14. Формы и валидация

## Цели урока
- Считывать данные форм
- Проверять ввод и показывать ошибки

## Форма
```html
<form id="form">
  <input type="text" name="name" placeholder="Имя">
  <input type="email" name="email" placeholder="Email">
  <input type="password" name="password" placeholder="Пароль">
  <button type="submit">Отправить</button>
  <p id="error" style="color:red"></p>
</form>
```

## Обработка отправки
```js
const form = document.querySelector("#form");
const error = document.querySelector("#error");

form.addEventListener("submit", (e) => {
  e.preventDefault();                         // не перезагружать страницу
  const data = Object.fromEntries(new FormData(form));
  const { name, email, password } = data;

  if (name.trim().length < 2) {
    error.textContent = "Имя слишком короткое";
    return;
  }
  if (!/^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(email)) {
    error.textContent = "Неверный email";
    return;
  }
  if (password.length < 8) {
    error.textContent = "Пароль минимум 8 символов";
    return;
  }
  error.textContent = "";
  console.log("Данные корректны", data);
});
```

## Встроенная валидация HTML
```html
<input type="email" required minlength="3" maxlength="50">
<input type="number" min="1" max="100">
<input pattern="[0-9]{9}" title="9 цифр">
```
JS: `form.checkValidity()`, `input.validity.valid`, `input.setCustomValidity("текст")`.

## Другие поля
```js
checkbox.checked;
select.value;
document.querySelector('input[name="gender"]:checked')?.value;
```

## Важно
Проверка на клиенте нужна для удобства пользователя. **Безопасность обеспечивает только серверная валидация.**

## Типичные ошибки
- Не отменили стандартную отправку формы
- Проверяют только на клиенте
- Не убирают пробелы перед проверкой (`trim()`)

## Практика
1. Форма регистрации с проверкой имени, email и пароля.
2. Индикатор надёжности пароля в реальном времени.
3. Форма с подтверждением пароля («пароли не совпадают»).

## Проверь себя
1. Что делает `FormData`?
2. Почему клиентской валидации недостаточно?
3. Как отменить перезагрузку страницы при отправке?

---
[← Урок 13](lesson-13.md) · [Программа курса](README.md) · [Урок 15 →](lesson-15.md)
