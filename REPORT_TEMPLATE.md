## Отчёт по заданию (Hugo + GitHub Pages)

### Что сделано

- Установлен Hugo на локальный компьютер.
- Создан сайт‑портфолио на Hugo.
- Добавлены страницы с большим объёмом контента: «Обо мне», «Проекты», «Посты/длинная статья».
- Сайт собран локально командой `hugo -D` (результат в папке `public/`).
- Выполнена ручная публикация собранного сайта на GitHub Pages.
- Настроен автоматический деплой на GitHub Pages через GitHub Actions.

### Ссылки

- Репозиторий с исходниками: https://github.com/whyamiherewhyamihere/frontend-site
- Развёрнутый GitHub Pages сайт: https://whyamiherewhyamihere.github.io/frontend-site/

### Скрипт (GitHub Actions) для деплоя

Workflow лежит в файле `.github/workflows/hugo-pages.yml`.

Что делает pipeline:

1. Триггерится по `push` в ветку `main` (и вручную через `workflow_dispatch`).
2. Скачивает исходники (`actions/checkout`).
3. Ставит Hugo (`peaceiris/actions-hugo`).
4. Конфигурирует GitHub Pages и получает корректный `base_url` (`actions/configure-pages`).
5. Собирает сайт командой `hugo --minify`.
6. Загружает папку `public/` как артефакт (`actions/upload-pages-artifact`).
7. Публикует артефакт в GitHub Pages (`actions/deploy-pages`).

### Примечание

Перед сдачей замените `USERNAME` и `REPO` на реальные значения.
