#### Основные команды PostgreSQL в интерактивном режиме:
```
\connect db_name – подключиться к базе с именем db_name
\du – список пользователей
\dp (или \z) – список таблиц, представлений, последовательностей, прав доступа к ним
\di – индексы
\ds – последовательности
\dt – список таблиц
\dt+ — список всех таблиц с описанием
\dt *s* — список всех таблиц, содержащих s в имени
\dv – представления
\dS – системные таблицы
\d+ – описание таблицы
\o – пересылка результатов запроса в файл
\l – список баз данных
\i – читать входящие данные из файла
\e – открывает текущее содержимое буфера запроса в редакторе (если иное не указано в окружении переменной EDITOR, то будет использоваться по умолчанию vi)
\d “table_name” – описание таблицы
\i запуск команды из внешнего файла, например \i /my/directory/my.sql
\pset – команда настройки параметров форматирования
\echo – выводит сообщение
\set – устанавливает значение переменной среды. Без параметров выводит список текущих переменных (\unset – удаляет).
\? – справочник psql
\help – справочник SQL
\q (или Ctrl+D) – выход с программы
```
#### Полезные команды
```
CREATE DATABASE db_name; - Создаем БД с названием db_name
CREATE USER db_user WITH PASSWORD 'db_user_pw'; - Создаем пользователя db_user с паролем db_user_pw
GRANT ALL PRIVILEGES ON DATABASE db_name to db_user; - Даем ВСЕ права пользователю db_user на базу db_name
SELECT rolname FROM pg_roles; - Посмотреть все роли в базе.
SELECT session_user; - Посмотреть текущего пользователя, под которым выполняется сеанс.

SELECT * FROM pg_stat_activity WHERE state = 'active'; - Получить все выполняемые запросы на сервере.
SELECT pg_cancel_backend(<pid of the process>); - kill неугодный процесс.
SELECT pg_terminate_backend(<pid of the process>); - если процесс не может быть kill, то пробуем это. 

SELECT pg_size_pretty(pg_database_size(current_database())); - получить красивый размер бд
SELECT pg_relation_size('accounts'); - получить размер конкретной таблицы
```
```
/usr/local/pgsql/data/postgresql.conf - Конфиг
```
