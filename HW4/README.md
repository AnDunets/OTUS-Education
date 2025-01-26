#HW - Работа с базами данных, пользователями и правами

Цель:
- создание новой базы данных, схемы и таблицы
- создание роли для чтения данных из созданной схемы созданной базы данных
- создание роли для чтения и записи из созданной схемы созданной базы данных

Шаг 1. Cоздать новый кластер PostgresSQL

Шаг 2. Зайти в созданный кластер под пользователем postgres
![image](https://github.com/user-attachments/assets/d335afc7-94ca-4dc8-8e90-463562412dd1)

Шаг 3. 
- Зайти в созданный кластер под пользователем postgres
- Создать новую базу данных
- Зайти в созданную базу данных под пользователем postgres
- Создать новую схему

![image](https://github.com/user-attachments/assets/4e094bc0-dacb-419f-b1d6-b8f6799fdab2)

Шаг 4.
- Создать новую таблицу t1 с одной колонкой c1 типа integer
- Вставить строку со значением c1=1

![image](https://github.com/user-attachments/assets/92dc3253-e2ea-43b0-b54c-08598ba932a2)

Шаг 5.
- Создать новую роль readonly
- Дать новой роли права на
  - подключение к базе данных
  - использование схемы
  - select для всех таблиц схемы
 
![image](https://github.com/user-attachments/assets/b8322399-17f8-4259-a92c-f0fc2c263b36)

Шаг 6.
- Создать пользователя testread с паролем test123
- Дать роль readonly пользователю testread
- Зайти под пользователем testread в базу данных testdb

![image](https://github.com/user-attachments/assets/5cd1aa85-9664-4d29-90e5-1ef5f3ff5edf)
Внесем корректировки в файл /etc/postgresql/16/main/pg_hba.conf:
![image](https://github.com/user-attachments/assets/6362ac47-d002-4ddd-9b18-e309afa4deca)
sudo service postgresql restart

Повторяем действия

![image](https://github.com/user-attachments/assets/eaa706ec-073e-4e76-89d8-df3752c2a82d)

Шаг 7. Выполните запрос select * from t1;

![image](https://github.com/user-attachments/assets/c30264ff-2105-4e57-9496-d8015b515d6f)

В доступе к данным таблицы t1 отказано.
При ее создании не указывали схему, поэтому она создалась внутри схемы public:

![image](https://github.com/user-attachments/assets/de84b818-cc72-460a-8a76-a7129269400a)

Из документации: По умолчанию такие таблицы (и другие объекты) автоматически помещаются в схему «public»

Шаг 8.
- Вернитесь в базу данных под пользователем postgres
- удалите таблицу t1

![image](https://github.com/user-attachments/assets/ca7e8ceb-9dd1-44f3-9d32-49085ad301c1)

Шаг 9.
- Создайте таблицу заново, но уже с явным указанием имени схемы
- Вставьте строку со значением c1=1
- Зайдите под пользователем testread в базу данных
- Сделайте select * from testdb.t1;

![image](https://github.com/user-attachments/assets/ae281698-c4ea-494e-a156-080962f4d364)

Отобразим перечень лиц, кому доступна таблица testdb.t1:

![image](https://github.com/user-attachments/assets/3f01188a-9ff7-4ef7-bde3-df2fd0ba3670)

Видим, что лист пуст, следовательно, на вновь сохданные таблицы необходимо выдавать права дополнительно.

![image](https://github.com/user-attachments/assets/e1f97602-dd6a-4235-a800-0e82e5b35366)

Шаг 10. Выполните команду create table t2(c1 integer); insert into t2 values (2);
Получаем ошибку, т.к. имеем лишь права на readonly:

![image](https://github.com/user-attachments/assets/9b95fd29-8cda-4b2f-8059-f60e639cb336)

search_path указывает в первую очередь на схему public. 
Схема public создается в каждой базе данных по умолчанию, поэтому grant на все действия в этой схеме дается роли public. 
Роль public добавляется всем новым пользователям, соответсвенно каждый пользователь может по умолчанию создавать объекты в схеме public любой базы данных

Шаг 11. Выполним команды:
  REVOKE CREATE on SCHEMA public FROM public; 
  REVOKE ALL on DATABASE otus4 FROM public;

Тем самым отозвали привелегии создания таблиц в схеме public, поэтому выполнение команды create table t3(c1 integer); insert into t2 values (2); выдает ошибку:

![image](https://github.com/user-attachments/assets/3c8220b8-2299-45f8-820a-b428eab2de74)
