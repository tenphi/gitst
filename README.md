# Git Subtree Helper

Консольная утилита для работы с git subtree.

## Установка

```bash
$ npm install -g gitst
```

## Описание

Git-репозиторий не содержит достаточной информации для восстановления информации о подключенных к нему других репозиториев, однако хранит информацию по префиксах (путях) по которым они были установлены. Используя соглашения о префиксах, git subtree восстанавливает всю необходимую информацию для предоставления более удобного интерфейса работы с subtree без каких либо конфигураций.

Соглашение о префиксах заключается в следующем: Префикс может быть любым, но последняя директория в пути должна иметь точно такое же имя, как origin подключенного репозитория без учета регистра. Имена origin'ов должны быть написаны исключительно маленькими буквами.

Например: Если мы подключаем репозиторий с именем **kit**, то его префикс (путь) должен иметь вид `path/to/kit`.

	$ git remote add kit user@git.repository.com/kit.git
	$ git subtree add --prefix=path/to/kit kit master

path/to/ **kit** - имя последней директории совпадает с именем origin'а **kit**.

## Команды

Отобразить все подключенные subtree:

	$ gitst list
	2 subtrees found:
	./dir2/kit1 <- kit1
	./dir2/kit2 <- kit2

Обновить subtree:

	$ gitst fetch {origin}

Забрать изменения из origin:

	$ gitst pull {origin} {branch}

Отправить изменния в origin:

	$ gitst push {origin} {branch}

Если вы выполняете команду **push** или **pull** без указания origin, важно помнить, что если вы выполняете команды для нескольких репозиториев одновременно, то **gitst** не получает информацию о ветке. Потому он считает, что нужно использовать ветку **master**.

Если одна из операций завершилась ошибкой, **gitst** выведет её на экран и завершит работу. Это даёт возможность последовательно решать конфликты не прибегая к ручному перечислению подключенных репозиториев.
