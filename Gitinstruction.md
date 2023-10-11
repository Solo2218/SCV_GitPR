![Logo](git-logo.png)

# Работа с Git

## 1. Проверка наличия установленного Git
В терминалы выполнить комманду `git --version`.
Если Git установлен, появиться сообщение с информация о версии программы, а иначе будет информация об ошибке.

![Git version](Git_version.png)

## 2. Установка Git
Загружаем последнию версию Git с [сайта](https://git-scm.com/downloads).
Устанавливаем с настройками по умолчанию.

## 3. Настройка Git
При первом использовании Git необходимо представиться.
Для этого нужно ввести в терминале 2 команды:
```
git config --global user.name «Ваше имя английскими буквами»
git config --global user.email «Ваша почта@example.com»
```

## 4. Создание Git-репозитория
Для того, чтобы инициализировать Git-репозиторий в текущем каталоге необходимо ввести команду `git init`. После чего в текущем каталоге появится скрытая папка с именем [.git] где и будет храниться сам репозиторий

## 5. Запись изменений в репозиторий
Для того, чтобы проверить есть ли изменения не занесенные в репозиторий используем команду `git status`. После выполнения данной команды появится сообщение с информацией о файле в котором есть изменения или об отсутствии каких-либо изменений.

![Git status](Git_status.png)

Для того чтобы начать отслеживать (добавить под версионный контроль) новый файл, используются команды:
```
git add .           # добавить в индекс все новые файлы в папке
git add file-name   # добавить в индекс указанный файл «Имя файла»
``` 
Для создания коммита в репозитории используем следующие команды:
```
git commit -m "Ваш комментарий"     # зафиксировать в коммите проиндексированные
                                      изменения (закоммитить), добавить сообщение
git commit -am "Ваш комментарий"    # проиндексировать отслеживаемые файлы и
                                      закоммитить, добавить сообщение
```
**Важно!** *Комада `git commit -am` закоммитит все отслеживаемые файлы, но не новые.*

Для того, чтобы посмотреть что именно было изменено необходимо ввести команду `git diff`. В результате будет выведено сообщение с тем, что именно было изменено.

![Git diff](Git_diff.png)

## 6. Просмотр истории изменений
После того, как вы создали несколько коммитов, вероятно вам понадобится возможность посмотреть что было сделано — историю коммитов. Для просмотра истории коммитов используем команды:
```
git log                        # Показывает историю комитов
git log --oneline              # Показывает историю комитов в сокращенном виде
git log --graph                # Показывает ветки и историю комитов
git log --graph --oneline      # Показывает ветки и историю комитов в сокращенном
                                 виде
```

После выполнения команды мы увидим историю изменений.

**Важно!** *Если история достаточно велика и полностью не отображается на экране терминала, её можно пролистать вниз с помощью стрелки пока не появиться надпись END для выхода из режима просмотра необходимо нажать `q`.*

## 7. Перемещение между сохранениями
Для того чтобы перейти на какой-либо из сохраненных комитов используем команду `git checkout "хеш-код"`. Где хеш-код это уникальный номер коммита, который можно посмотреть с помощью команды `git log`.

**Важно!** *Не обязательно использовать весь хеш-код, достаточно использовать первые 3-7 символов*

## 8. Игнорирование файлов
Для того, чтобы исключить из отслеживания в репозитории определенные файлы или папки необходимо создать там файл ***.gitignore*** и записать в него их названия или шаблоны, соответствующие таким файлам или папкам.

## 9. Создание веток в Git
По умолчанию имя основной ветки в Git - **master**
Создать ветку можно одной из команд:
```
git branch <имя новой ветки>
git checkout -b <имя новой ветки>
git switch -c <имя новой ветки>
```
**Важно!** *При использовании команды `git checkout -b <имя новой ветки>` или `git switch -c <имя новой ветки>` кроме того, что создастся новая ветка, также  произойдет переключение на эту ветку.*

Список веток в репозитории можно посмотреть с помощью команды `git branch`.
Текущая ветка будет отмечена звёздочкой: **\* master**.

![Git branch](Git_branch.png)

Для переключения между ветками используются команды:
```
git switch <имя ветки>
git checkout <имя ветки>
```

**Примечание:** *Команда `git switch` была добавлена в Git версии 2.23 для облегчения запоминания пользователями.*

## 10. Слияние веток и разрешение конфликтов
Для того, чтобы объединить две ветки сначало нужно переключиться на ту ветку в которую мы будем слиять коммит. Это можно сделать с помощью команды `git switch <имя ветки>`. 
Для объединения веток необходимо использовать команду:
```
git merge <имя ветки с которой берем изменения>
```

В результате увидим сообщение о слиянии двух веток. 

![Git merge success](Git_merge_success.png)

Иногда процесс не проходит гладко. Если вы изменили одну и ту же часть одного и того же файла по-разному в двух объединяемых ветках, Git не сможет их чисто объединить и тогда возникает конфликт. 

![Git merge fail](Git_merge_fail.png)

Для разрешения конфликта Git выдаст соответствующие сообщение с отображением строк в которых произошел конфликт. Например в IDE *Visual Studio Code* открывается интерфейс:

![iterface](Git_conflict.png)

И предлогается 4 варианта действий:
* *Accept Current Change* - Принять изменения из основной ветви
* *Accept Incomimg Change* - Принять изменения из входящей ветви
* *Accept Both Changes* - Принять изменения из обеих ветвей
* *Compare Changes* - Сравнить изменения (Только просмотр)

После выбора одного из 3 вариантов разрешения конфликта произойдет слияние.

**Важно!** *После разрешения конфликта обязательно выполнить команду `git commit -am` для фиксации изменений либо `git merge --abort` если хотим отменить слияние*.

## 11. Удаление веток
После того как мы закончили работу с какой-либо веткой и слили с основной её необходимо удалить. Для удаления ветки используется команда:
```
git branch -d <имя ветки>
```
После чего увидим сообщение о удалении.

![Delete success](Git_delete_branch.png)

**Примечание:** *Если в удаляемой ветке есть коммиты не слитые с другой веткой будет выведено сообщение об ошибке и рекомендация для использования команды `git branch -D <имя ветки>` для принудительного удаления.*

![Delete fail](Git_delete_branch_fail.png)

**Важно!** *Нельзя удалить ветку в которой вы находитесь, необходимо переключиться на любую другую ветку и только потом удалять.*