# Лабораторная работа №6. Система контроля версий

## Цель работы

Изучение базовых возможностей системы управления версиями, получение опыта работы с Git API, а также с локальным и удалённым репозиторием.

## Текст задания

1. Создать аккаунт на сайте GitHub.
2. Сделать копию в личное хранилище из https://github.com/Kurtyanik/LR6/ (Fork).
3. Установить Git.
4. Настроить клиент git: имя пользователя (Группа Фамилия И.О.) и email.
5. Клонировать личный удалённый репозиторий на компьютер.
6. Добавить файл через интерфейс GitHub, подтянуть изменения в локальный репозиторий.
7. Получить историю операций для каждой из веток.
8. Просмотреть последние изменения.
9. Выполнить слияние в ветку master, разрешив конфликт.
10. Удалить побочную ветку после успешного слияния.
11. Сделать несколько изменений и зафиксировать их с комментариями.
12. Сделать откат коммита.
13. Создать ветку для отчёта.
14. Оформить отчёт в README.md с использованием markdown: снимки экрана, лог команд.
15. Получить форматированную историю операций (сокращённый хэш + дата + автор + комментарий), добавить в отчёт, сделать финальный коммит.
16. Отправить локальные изменения в GitHub.

## Описание хода выполнения

### 1. Создание аккаунта на GitHub

Зарегистрирован аккаунт на сайте https://github.com. Имя пользователя: balka1101.

![Аккаунт GitHub](screenshots/01_account.png)

### 2. Fork репозитория

Со страницы https://github.com/Kurtyanik/LR6/ нажата кнопка **Fork**, копия репозитория создана в личном хранилище: `https://github.com/balka1101/LR6`.

![Fork](screenshots/02_fork.png)

### 3. Установка Git

Git установлен с сайта https://git-scm.com/. Версия проверена командой `git --version`.

![Установка Git](screenshots/03_install.png)

### 4. Настройка клиента

Указаны имя пользователя в формате «Группа Фамилия И.О.» и адрес электронной почты.

```bash
git config --global user.name "4517 Балакин К.А."
git config --global user.email "kostabalakin315@gmail.com"
git config --list
```

![Настройка git](screenshots/04_config.png)

### 5. Клонирование репозитория

Личный удалённый репозиторий клонирован на компьютер.

```bash
git clone https://github.com/balka1101/LR6.git
cd LR6
```

![Клонирование](screenshots/05_clone.png)

### 6. Добавление файла через интерфейс GitHub

Через веб-интерфейс GitHub добавлен новый файл (**Add file → Create new file**) и выполнен коммит. Затем изменения подтянуты в локальный репозиторий.

```bash
git pull
```

![Файл на GitHub](screenshots/06_github_file.png)
![git pull](screenshots/06_pull.png)

### 7. История операций для каждой из веток

Список веток и история коммитов каждой из них.

```bash
git branch -a
git log master
git log feature
git log --oneline --graph --all
```

![История веток](screenshots/07_log.png)

### 8. Просмотр последних изменений

```bash
git show
git diff HEAD~1 HEAD
```

![Последние изменения](screenshots/08_show.png)

### 9. Слияние в ветку master с разрешением конфликта

Выполнено переключение на master и слияние побочной ветки. При слиянии возник конфликт в файле conflict.txt: в файле присутствовали маркеры `<<<<<<<`, `=======`, `>>>>>>>`. Конфликт разрешён вручную в редакторе (оставлен нужный вариант содержимого), после чего файл добавлен в индекс и создан коммит слияния.

```bash
git checkout master
git merge feature
git status
git add conflict.txt
git commit -m "Merge: разрешён конфликт в conflict.txt"
```

![Конфликт](screenshots/09_conflict.png)
![Разрешение конфликта в редакторе](screenshots/09_resolve.png)
![Результат слияния](screenshots/09_merge_done.png)

### 10. Удаление побочной ветки

После успешного слияния побочная ветка удалена.

```bash
git branch -d feature
git branch
```

![Удаление ветки](screenshots/10_delete_branch.png)

### 11. Изменения и коммиты с комментариями

Внесено несколько изменений в файлы, каждое зафиксировано отдельным коммитом с поясняющим комментарием.

```bash
git add .
git commit -m "Добавлен файл <...>"
git add .
git commit -m "Изменён файл <...>"
git add .
git commit -m "Исправлено <...>"
```

![Коммиты](screenshots/11_commits.png)

### 12. Откат коммита

Выполнен откат последнего коммита с созданием нового коммита, отменяющего изменения.

```bash
git log --oneline
git revert HEAD
```

![Откат коммита](screenshots/12_revert.png)

### 13. Создание ветки для отчёта

```bash
git checkout -b report
mkdir screenshots
```

Снимки экрана размещены в папке `screenshots`.

![Ветка report](screenshots/13_report_branch.png)

### 14. Оформление отчёта

Отчёт оформляется в файле `README.md` с использованием markdown-синтаксиса. В процессе работы периодически выполнялись коммиты с комментариями.

```bash
git add README.md screenshots
git commit -m "Добавлены разделы отчёта: шаги 1-8"
git add README.md screenshots
git commit -m "Добавлены разделы отчёта: шаги 9-13, лог команд"
```

### 15. История операций в форматированном виде

Получена история в формате: сокращённый хэш, дата, имя автора, комментарий.

```bash
git log --pretty=format:"%h %ad %an %s" --date=short
```

История:

```text
<ВСТАВЬТЕ СЮДА ВЫВОД КОМАНДЫ>
```

![Форматированная история](screenshots/15_pretty_log.png)

### 16. Отправка изменений в GitHub

Локальные изменения отправлены в удалённый репозиторий.

```bash
git push origin master
git push -u origin report
```

![git push](screenshots/16_push.png)

## Лог команд

```bash
git --version
git config --global user.name "4517 Балакин К.А."
git config --global user.email "<ВАШ_EMAIL>"
git config --list
git clone https://github.com/<ВАШ_ЛОГИН>/LR6.git
cd LR6
git pull
git branch -a
git log master
git log feature
git log --oneline --graph --all
git show
git diff HEAD~1 HEAD
git checkout master
git merge feature
git status
git add feature
git commit -m "Merge: разрешён конфликт в <ИМЯ_ФАЙЛА>"
git branch -d feature
git add .
git commit -m "Добавлен файл <...>"
git add .
git commit -m "Изменён файл <...>"
git revert HEAD
git checkout -b report
git add README.md screenshots
git commit -m "Добавлены разделы отчёта: шаги 1-8"
git add README.md screenshots
git commit -m "Добавлены разделы отчёта: шаги 9-13, лог команд"
git log --pretty=format:"%h %ad %an %s" --date=short
git add README.md
git commit -m "Финальная версия отчёта"
git push origin master
git push -u origin report
```

## Выводы

В ходе лабораторной работы изучены базовые возможности системы контроля версий Git и сервиса GitHub. Получены практические навыки создания форка и клонирования репозитория, работы с ветками, слияния с разрешением конфликтов, фиксации изменений с комментариями, отката коммитов, просмотра и форматирования истории операций, а также синхронизации локального и удалённого репозиториев.
