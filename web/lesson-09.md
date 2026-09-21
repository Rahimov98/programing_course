# Веб · Урок 9. Блочная модель

## Цели урока
- Понять content → padding → border → margin
- Использовать box-sizing
- Управлять шириной, высотой и отступами

## Теория

**Блочная модель**
```
+---------------------------+
|         margin            |
|  +---------------------+  |
|  |       border        |  |
|  |  +---------------+  |  |
|  |  |    padding    |  |  |
|  |  |  +---------+  |  |  |
|  |  |  | content |  |  |  |
|  |  |  +---------+  |  |  |
|  |  +---------------+  |  |
|  +---------------------+  |
+---------------------------+
```

```css
.box {
  width: 200px;
  height: 100px;
  padding: 20px;           /* внутри, вокруг content */
  border: 2px solid #333;
  margin: 10px;            /* снаружи */
}
```

**Сокращения**
```css
padding: 10px;                    /* все стороны */
padding: 10px 20px;               /* верх/низ | лево/право */
padding: 10px 20px 15px 5px;      /* верх право низ лево */
margin: 0 auto;                   /* центрирование блочного элемента */
```

**box-sizing**
```css
* {
  box-sizing: border-box;  /* width включает padding и border */
}
```
По умолчанию `content-box` — width только content, из‑за этого «ломается» вёрстка.

**display**
- `block` — на всю ширину, перенос строки
- `inline` — в строке, width/height не работают
- `inline-block` — в строке, но с размерами
- `none` — скрыть

## Типичные ошибки
- Забыли `box-sizing: border-box`
- Margin collapse (вертикальные margin схлопываются)
- Путаница padding и margin

## Практика
1. Создайте карточку с padding, border и margin.
2. Включите `border-box` глобально.
3. Отцентрируйте блок через `margin: 0 auto` (нужна ширина).

## Проверь себя
1. В каком порядке идут content, padding, border, margin?
2. Что меняет `box-sizing: border-box`?
3. Чем margin отличается от padding?

---
[← Урок 8](lesson-08.md) · [Программа курса](README.md) · [Урок 10 →](lesson-10.md)
