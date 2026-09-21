# JavaScript · Урок 22. Node.js: основы

## Цели урока
- Запускать JavaScript вне браузера
- Работать с модулями, файлами и `npm`

## Установка
Скачайте LTS-версию с [nodejs.org](https://nodejs.org/). Проверка:
```bash
node --version
npm --version
```

## Первая программа
Файл `app.js`:
```js
console.log("Привет из Node.js!");
console.log(process.argv);     // аргументы командной строки
```
Запуск: `node app.js`

## Модули
В Node.js используются ES-модули (в `package.json` добавьте `"type": "module"`) или CommonJS.
```js
// ES-модули
import fs from "node:fs/promises";
import path from "node:path";
import { add } from "./math.js";

// CommonJS
const os = require("os");
```

## Работа с файлами
```js
import fs from "node:fs/promises";

await fs.writeFile("notes.txt", "Первая строка\n", "utf-8");
await fs.appendFile("notes.txt", "Вторая строка\n");
const text = await fs.readFile("notes.txt", "utf-8");
console.log(text);
```

## npm и пакеты
```bash
npm init -y                # создать package.json
npm install lodash         # установить пакет
npm install -D nodemon     # dev-зависимость
npm install                # установить всё из package.json
```
В `package.json` можно добавить скрипты:
```json
"scripts": { "start": "node app.js", "dev": "nodemon app.js" }
```
Запуск: `npm run dev`.

## Переменные окружения
```js
const port = process.env.PORT || 3000;
```
Секреты храните в `.env`, который **не** загружают на GitHub (добавьте в `.gitignore`).

## Типичные ошибки
- `require` в файле с `"type": "module"`
- Папку `node_modules` загружают в репозиторий — добавьте в `.gitignore`
- Нет `package.json` в папке проекта

## Практика
1. Скрипт, считывающий текстовый файл и считающий в нём слова.
2. Утилита командной строки: принимает число из `process.argv` и выводит его факториал.
3. Установите пакет `chalk` и выведите цветной текст.

## Проверь себя
1. Чем Node.js отличается от браузерного JS?
2. Что хранится в `package.json`?
3. Как запустить скрипт из `scripts`?

---
[← Урок 21](lesson-21.md) · [Программа курса](README.md) · [Урок 23 →](lesson-23.md)
