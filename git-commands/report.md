# Отчёт по выполненным командам (Git Bash)

Дата: 27 декабря 2025

## Цель
Создать локальный Git‑репозиторий, добавить и закоммитить файлы, подключить удалённый репозиторий на GitHub и синхронизировать изменения (push/pull), а также выполнить операции со staging, ветками и merge.

## Окружение
- ОС: Windows
- Терминал: Git Bash (MINGW64)
- Рабочая папка: `C:/Users/User/demo-repo`
- Основная ветка: `master`

## Хронология команд (что делалось и зачем)

### 1) Переход в папку проекта
 `cd demo-repo`
   - Переход в каталог проекта, где должен быть репозиторий.

### 2) Инициализация Git‑репозитория
 `git init`
   - Создание пустого репозитория (папка `.git/`).
   - Результат: Git сообщил `Initialized empty Git repository ...`.

### 3) Проверка содержимого каталога
 `ls`
   - Просмотр файлов в текущей папке.

 `ls -la`
   - Корректный вывод содержимого с правами/владельцами.
   - Результат: видно `.git/` и служебные директории.

### 4) Проверка статуса репозитория
 `git status`
   - Проверка состояния репозитория.
   - Результат: ветка `master`, коммитов нет, отслеживаемых файлов нет.

### 5) Создание и первый коммит файла
 `touch readme.txt`
   - Создание нового файла `readme.txt`.

 `nano readme.txt`
   - Редактирование файла (ввод содержимого).

 `git status`
   - Проверка: файл `readme.txt` отображается как `Untracked` (не отслеживается Git).

 `git add readme.txt`
   - Добавление файла в staging area (подготовка к коммиту).
   - Результат: предупреждение про окончания строк: `LF will be replaced by CRLF` (типично для Windows).

 `git status`
   - Проверка: `readme.txt` в списке “Changes to be committed”.

 `git commit -m "first file"`
   - Создание первого коммита.
   - Результат: создан root‑commit `51bb365`.

 `git status` (дважды)
   - Проверка: рабочее дерево чистое (`working tree clean`).

### 6) Изменение файла и добавление всех *.txt
 `nano readme.txt`
   - Редактирование `readme.txt`.

 `git status`
   - Проверка: `readme.txt` изменён, но не добавлен в staging (`Changes not staged for commit`).

16.   - Добавление изменённого файла в staging.
   - Результат: снова предупреждение `LF -> CRLF`.

 `git add '*.txt'`
   - Добавление в staging всех файлов с расширением `.txt`.
   - Результат: в staging попали также `readme after.txt` и `readme now.txt` (предупреждения `LF -> CRLF`).

 `git status`
   - Проверка: к коммиту подготовлены 3 изменения: 2 новых файла и модификация `readme.txt`.

   - Коммит всех подготовленных изменений.
   - Результат: коммит `549cd9b`, добавлены `readme after.txt` и `readme now.txt`.

### 7) Просмотр истории
 `git log`
   - Просмотр списка коммитов.

 `git log --summary`
   - Просмотр коммитов с кратким summary по изменённым/созданным файлам.

### 8) Подключение удалённого репозитория и отправка изменений
 `git remote add origin https://github.com/whyamiherewhyamihere/test-repo.git`
   - Добавление удалённого репозитория с именем `origin`.

 `git push -u origin master`
   - Результат: ветка `master` создана на origin, upstream настроен.

 `git push -u origin master` (повторно)
   - Повторная отправка.
   - Результат: `Everything up-to-date`.

### 9) Получение изменений с удалённого репозитория
 `git pull origin master`
   - Забрать изменения с GitHub.
   - Результат: `Fast-forward` до коммита `486fe3e`, в `readme.txt` добавились строки.

### 10) Попытки посмотреть diff 
 `git diff HEAD`
   - Попытка посмотреть различия относительно `HEAD`.
   - Результат: вывода нет (на тот момент либо нет локальных изменений, либо diff пустой).

 `nano readme.txt`
   - Редактирование `readme.txt`.

 `git diff HEAD`
   - Повторный просмотр diff.


### 11) Создание папки и файла, staging и отмена staging
 `mkdir folder`
   - Создание каталога `folder`.

 `touch folder/bye.txt`
   - Создание файла `folder/bye.txt`.

 `git status`
   - Проверка: папка `folder/` отображается как `Untracked`.

 `git add folder/bye.txt`
   - Добавление нового файла в staging.


### 12) Просмотр staged diff и снятие файла со staging
 `git diff --staged`
   - Просмотр того, что добавлено в staging.
   - Результат: показан новый пустой файл `folder/bye.txt`. `git reset folder/bye.txt`
   - Снятие файла со staging (unstage).

 `git diff`
   - Просмотр незакоммиченных изменений в рабочей директории.

### 13) Откат локальных изменений файла
 `git checkout -- readme.txt`
   - Откат изменений в `readme.txt` до состояния последнего коммита (discard changes).

 `git status`
   - Проверка: изменений нет, но `folder/` всё ещё untracked.

### 14) Работа с веткой clean_up, коммит и merge
 `git branch clean_up`
   - Создание новой ветки `clean_up`.

 (переключение на ветку `clean_up` и коммит)
   - В логе видно, что на ветке `clean_up` был создан коммит:
     - `[clean_up 2f1f3ee] cleanup`
     - Удалены файлы `readme after.txt` и `readme now.txt`.
   
 `git checkout master`
   - Возврат на ветку `master`.

 `git merge clean_up`
   - Слияние ветки `clean_up` в `master`.
   - Результат: `Fast-forward`, удалённые txt‑файлы удалились и в master.

 `git branch -d clean_up`
   - Удаление ветки `clean_up` локально (после успешного merge).

### 15) Отправка изменений на GitHub
 `git push`
   - Отправка новых коммитов в удалённый репозиторий.
   - Результат: `master` на origin обновился до `2f1f3ee`.



## Итог
- Репозиторий инициализирован и наполнен коммитами.
- Настроен `origin` и выполнены `push/pull` с GitHub.
- Отработаны базовые операции: staging/unstage, просмотр логов, создание ветки, merge и удаление ветки.
