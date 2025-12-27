# Hugo Portfolio (GitHub Pages)

Этот репозиторий — исходники Hugo‑сайта портфолио и GitHub Actions workflow для деплоя на GitHub Pages.

## Локальный запуск

1) Установите Hugo Extended (рекомендуется) под Windows.
2) В корне проекта:

```powershell
hugo version
hugo server -D
```

Сайт будет доступен на `http://localhost:1313/`.

## Сборка

```powershell
hugo -D
```

Результат сборки появится в папке `public/`.

## Ручная публикация на GitHub Pages (для отчёта)

Один из простых вариантов «вручную»:

1) Соберите сайт:

```powershell
hugo -D --minify
```

2) Скопируйте содержимое `public/` в папку `docs/` в корне репозитория.
3) Закоммитьте `docs/` и запушьте в `main`.
4) В GitHub → Settings → Pages → Source выберите: **Deploy from a branch** → `main` → `/docs`.

После этого можно переключиться на деплой через Actions (ниже).

## Деплой на GitHub Pages через Actions

Workflow лежит в `.github/workflows/hugo-pages.yml`.

В GitHub:
- Settings → Pages → Build and deployment → Source: **GitHub Actions**.
- Репозиторий должен быть публичным (или нужен GitHub Pro/Team для private Pages).

После пуша в `main` Actions соберёт сайт и опубликует его в Pages.
