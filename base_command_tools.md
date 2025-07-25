#### Утилиты (программы) PosgreSQL:
```
createdb и dropdb – создание и удаление базы данных (соответственно)
```
```
createuser и dropuser – создание и удаление пользователя (соответственно)
```
```
pg_ctl – программа предназначенная для решения общих задач управления (запуск, останов, настройка параметров и т.д.)
```
```
postmaster – многопользовательский серверный модуль PostgreSQL (настройка уровней отладки, портов, каталогов данных)
```
```
initdb – создание новых кластеров PostgreSQL
```
```
initlocation – программа для создания каталогов для вторичного хранения баз данных
```
```
vacuumdb – физическое и аналитическое сопровождение БД
```
```
pg_dump – архивация и восстановление данных
```
```
pg_dumpall – резервное копирование всего кластера PostgreSQL
```
```
pg_restore – восстановление БД из архивов (.tar, .tar.gz)
```
#### Примеры создания резервных копий:
Создание бекапа базы mydb, в сжатом виде
```
pg_dump -h localhost -p 5440 -U someuser -F c -b -v -f mydb.backup mydb
```
Создание бекапа базы mydb, в виде обычного текстового файла, включая команду для создания БД
```
pg_dump -h localhost -p 5432 -U someuser -C -F p -b -v -f mydb.backup mydb
```
Создание бекапа базы mydb, в сжатом виде, с таблицами которые содержат в имени payments
```
pg_dump -h localhost -p 5432 -U someuser -F c -b -v -t *payments* -f payment_tables.backup mydb
```
Дамп данных только одной, конкретной таблицы. Если нужно создать резервную копию нескольких таблиц, то имена этих таблиц перечисляются с помощью ключа -t для каждой таблицы.
```
pg_dump -a -t table_name -f file_name database_name
```
Создание резервной копии с сжатием в gz
```
pg_dump -h localhost -O -F p -c -U postgres mydb | gzip -c > mydb.gz
```

#### Восстановление таблиц из резервных копий (бэкапов):
```
psql — восстановление бекапов, которые хранятся в обычном текстовом файле (plain text);
pg_restore — восстановление сжатых бекапов (tar);
```
#### Восстановление всего бекапа с игнорированием ошибок
```
psql -h localhost -U someuser -d dbname -f mydb.sql
```
#### Восстановление всего бекапа с остановкой на первой ошибке
```
psql -h localhost -U someuser —set ON_ERROR_STOP=on -f mydb.sql
```
Для восстановления из tar-архива нам понадобиться сначала создать базу с помощью CREATE DATABASE mydb; (если при создании бекапа не была указана опция -C) и восстановить
```
pg_restore —dbname=mydb —jobs=4 —verbose mydb.backup
```
Восстановление резервной копии БД, сжатой gz
```
gunzip mydb.gz
psql -U postgres -d mydb -f mydb
```