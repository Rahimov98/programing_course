# Веб · Урок 10. Позиционирование

## Цели урока
- Использовать position: static, relative, absolute, fixed, sticky
- Понимать containing block и z-index
- Создавать оверлеи и «липкие» элементы

## Теория

**position**
```css
.static   { position: static; }    /* по умолчанию */
.relative { position: relative; top: 10px; left: 20px; }
.absolute { position: absolute; top: 0; right: 0; }
.fixed    { position: fixed; bottom: 20px; right: 20px; }
.sticky   { position: sticky; top: 0; }
```

- **relative** — сдвиг относительно своего места, место сохраняется
- **absolute** — относительно ближайшего предка с position ≠ static
- **fixed** — относительно окна браузера
- **sticky** — как relative, пока не «прилипнет» при скролле

**z-index** (только для positioned)
```css
.modal { position: fixed; z-index: 1000; }
.overlay { position: fixed; z-index: 999; }
```

**Пример: кнопка «наверх»**
```css
.back-to-top {
  position: fixed;
  bottom: 24px;
  right: 24px;
  z-index: 50;
}
```

**Центрирование absolute**
```css
.modal {
  position: fixed;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}
```

## Типичные ошибки
- Absolute без relative-родителя → позиционируется от body/viewport
- z-index без position
- Sticky не работает из‑за overflow у родителя

## Практика
1. Сделайте «липкую» шапку (`position: sticky`).
2. Кнопку «наверх» в правом нижнем углу (`fixed`).
3. Блок, сдвинутый на 20px вниз относительно себя (`relative`).

## Проверь себя
1. Чем absolute отличается от fixed?
2. Относительно чего позиционируется absolute?
3. Когда нужен z-index?

---
[← Урок 9](lesson-09.md) · [Программа курса](README.md) · [Урок 11 →](lesson-11.md)
