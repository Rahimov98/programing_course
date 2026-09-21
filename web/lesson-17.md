# Веб · Урок 17. Git и GitHub Pages

## Цели урока
- Инициализировать репозиторий и делать коммиты
- Выложить сайт на GitHub Pages
- Понимать базовый workflow

## Теория

**Базовые команды**
```bash
git init
git add .
git commit -m "Первый коммит: структура сайта"
git branch -M main
git remote add origin https://github.com/username/repo.git
git push -u origin main
```

**Повседневная работа**
```bash
git status
git add index.html styles.css
git commit -m "Добавлена адаптивная сетка"
git push
```

**GitHub Pages**
1. Репозиторий на GitHub
2. Settings → Pages → Source: Deploy from a branch
3. Branch: `main`, folder: `/` (или `/docs`)
4. Сайт будет доступен по адресу:
   `https://username.github.io/repo-name/`

**Важно для Pages**
- Файл `index.html` в корне (или в docs/)
- Относительные пути к CSS/картинкам
- Иногда нужно подождать 1–2 минуты после push

**.gitignore**
```
.DS_Store
node_modules/
*.log
```

**Полезные привычки**
- Коммиты мелкие и с понятными сообщениями
- Не коммитить пароли и токены
- `git pull` перед работой, если репозиторий общий

## Типичные ошибки
- Забыли `git add` перед commit
- Абсолютные пути к файлам → на Pages ломается
- Push не в ту ветку

## Практика
1. Создайте репозиторий и закоммитьте свой учебный сайт.
2. Включите GitHub Pages.
3. Откройте сайт по выданной ссылке и проверьте, что стили подгрузились.

## Проверь себя
1. Чем `git add` отличается от `git commit`?
2. Что такое remote origin?
3. Где лежит index.html для GitHub Pages?

---
[← Урок 16](lesson-16.md) · [Программа курса](README.md) · [Урок 18 →](lesson-18.md)
