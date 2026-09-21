# Веб · Урок 14. Переходы и анимации

## Цели урока
- Добавлять плавные переходы (transition)
- Создавать простые анимации (@keyframes)
- Не перегружать интерфейс эффектами

## Теория

**Transition**
```css
.button {
  background: #3366ff;
  transition: background 0.2s ease, transform 0.2s ease;
}
.button:hover {
  background: #2952cc;
  transform: translateY(-2px);
}
```

Свойства: `transition-property`, `duration`, `timing-function` (ease, linear, ease-in-out), `delay`.

**Transform**
```css
transform: translateX(10px);
transform: scale(1.05);
transform: rotate(5deg);
transform: translate(-50%, -50%) scale(1.1);
```

**@keyframes**
```css
@keyframes fadeIn {
  from { opacity: 0; transform: translateY(10px); }
  to   { opacity: 1; transform: translateY(0); }
}

.card {
  animation: fadeIn 0.4s ease forwards;
}
```

**Управление**
```css
animation-name: fadeIn;
animation-duration: 0.4s;
animation-timing-function: ease;
animation-delay: 0.1s;
animation-iteration-count: 1;  /* или infinite */
animation-fill-mode: forwards;
```

**prefers-reduced-motion**
```css
@media (prefers-reduced-motion: reduce) {
  * {
    animation: none !important;
    transition: none !important;
  }
}
```

## Типичные ошибки
- Анимация всего подряд — раздражает
- Слишком долгие transition (>0.4s для UI)
- Анимация layout-свойств (width, height) вместо transform/opacity

## Практика
1. Кнопка с плавной сменой фона и лёгким подъёмом при hover.
2. Появление карточки с fadeIn.
3. Учтите `prefers-reduced-motion`.

## Проверь себя
1. Чем transition отличается от animation?
2. Почему лучше анимировать transform и opacity?
3. Зачем prefers-reduced-motion?

---
[← Урок 13](lesson-13.md) · [Программа курса](README.md) · [Урок 15 →](lesson-15.md)
