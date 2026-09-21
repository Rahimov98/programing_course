# JavaScript · Урок 21. localStorage

## Цели урока
- Сохранять данные в браузере между сессиями

## Хранилища
| | localStorage | sessionStorage |
|---|---|---|
| Время жизни | пока пользователь не очистит | до закрытия вкладки |
| Объём | ~5 МБ | ~5 МБ |
| Тип данных | только строки | только строки |

## Основные методы
```js
localStorage.setItem("theme", "dark");
localStorage.getItem("theme");       // "dark" (или null)
localStorage.removeItem("theme");
localStorage.clear();
localStorage.length;
```

## Сохранение объектов
Значения хранятся только как строки, поэтому нужен JSON:
```js
const tasks = [{ id: 1, title: "Купить хлеб", done: false }];
localStorage.setItem("tasks", JSON.stringify(tasks));

const saved = JSON.parse(localStorage.getItem("tasks")) ?? [];
```

## Удобные функции
```js
const storage = {
  get(key, fallback = null) {
    try {
      return JSON.parse(localStorage.getItem(key)) ?? fallback;
    } catch {
      return fallback;
    }
  },
  set(key, value) {
    localStorage.setItem(key, JSON.stringify(value));
  },
};
```

## Пример: запоминаем тему
```js
const saved = localStorage.getItem("theme") || "light";
document.body.dataset.theme = saved;

toggleBtn.addEventListener("click", () => {
  const next = document.body.dataset.theme === "light" ? "dark" : "light";
  document.body.dataset.theme = next;
  localStorage.setItem("theme", next);
});
```

## Безопасность
Не храните пароли, токены и персональные данные в `localStorage`: любой скрипт на странице может их прочитать.

## Типичные ошибки
- Сохраняют объект без `JSON.stringify` → `"[object Object]"`
- Не обрабатывают `null` при первом запуске
- Хранилище может быть недоступно (приватный режим, переполнение) — оборачивайте в `try/catch`

## Практика
1. Запоминайте имя пользователя и приветствуйте при повторном посещении.
2. Сохраняйте список заметок между перезагрузками.
3. Счётчик посещений страницы.

## Проверь себя
1. Чем `localStorage` отличается от `sessionStorage`?
2. Как сохранить массив объектов?
3. Почему нельзя хранить там пароли?

---
[← Урок 20](lesson-20.md) · [Программа курса](README.md) · [Урок 22 →](lesson-22.md)
