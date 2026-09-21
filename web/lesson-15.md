# Веб · Урок 15. Псевдоклассы и псевдоэлементы

## Цели урока
- Использовать :hover, :focus, :nth-child и другие
- Создавать декоративные элементы через ::before / ::after
- Улучшать доступность фокуса

## Теория

**Псевдоклассы (состояние)**
```css
a:hover { color: #3366ff; }
a:focus { outline: 2px solid #3366ff; }
a:visited { color: purple; }
input:focus { border-color: #3366ff; }
input:disabled { opacity: 0.5; }
button:active { transform: scale(0.98); }
```

**Структурные**
```css
li:first-child { }
li:last-child { }
li:nth-child(odd) { background: #f5f5f5; }
li:nth-child(3n) { }           /* каждый 3-й */
p:not(.intro) { }
```

**Псевдоэлементы**
```css
.card::before {
  content: "";
  position: absolute;
  top: 0; left: 0;
  width: 4px; height: 100%;
  background: #3366ff;
}

.quote::before { content: "«"; }
.quote::after  { content: "»"; }

input::placeholder { color: #999; }
::selection { background: #3366ff; color: #fff; }
```

**Важно**
- У `::before` / `::after` обязательно `content` (хотя бы `""`)
- Для позиционирования псевдоэлемента родителю часто нужен `position: relative`

**Фокус**
Не убирайте `outline` без замены — пользователи с клавиатуры потеряют видимость фокуса.
```css
button:focus-visible {
  outline: 2px solid #3366ff;
  outline-offset: 2px;
}
```

## Типичные ошибки
- `content` забыт
- Стили только для :hover без :focus
- Слишком специфичные nth-child

## Практика
1. Ссылки меняют цвет при hover и focus.
2. Чередование фона строк списка через nth-child.
3. Декоративная полоска слева у карточки через ::before.

## Проверь себя
1. Чем псевдокласс отличается от псевдоэлемента?
2. Зачем `content` у ::before?
3. Почему нельзя просто убрать outline?

---
[← Урок 14](lesson-14.md) · [Программа курса](README.md) · [Урок 16 →](lesson-16.md)
