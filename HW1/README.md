#HW - Работа с уровнями изоляции транзакции в PostgreSQL

Цель:
- научиться работать с Google Cloud Platform на уровне Google Compute Engine (IaaS)
- научиться управлять уровнем изолции транзации в PostgreSQL и понимать особенность работы уровней read commited и repeatable read

Шаг 1. Создать ВМ с Ubuntu 20.04/22.04 или развернуть докер любым удобным способом

Ключ был создан в приложении PuTTYgen.
Виртуальная машина была создана в ЯО, подключение к ней производилось через приложение PuTTY.

Шаг 2. Поставить PostgreSQL
Для установки PostgreSQL на ВМ применялась команда:
    sudo apt install postgresql

Шаг 3. Получить параметры кластера
     sudo pg_lsclusters
![image](https://github.com/user-attachments/assets/a5173a57-9829-4ca6-b52e-22f47d296edf)

Шаг 4. Подключение к БД под пользователем postgres
     sudo -u postgres psql

Шаг 5. Выключить auto commit
![image](https://github.com/user-attachments/assets/45e46868-ca4f-45d8-b956-656920ea04af)

Шаг 6. В первой сессии новую таблицу и наполнить ее данными 
    create table persons(id serial, first_name text, second_name text); 
    insert into persons(first_name, second_name) values('ivan', 'ivanov'); 
    insert into persons(first_name, second_name) values('petr', 'petrov'); 
    commit;
![image](https://github.com/user-attachments/assets/a535ef24-70bf-43f4-b92e-dfa675eb8774)

Шаг 7. Посмотреть текущий уровень изоляции
    show transaction isolation level;
![image](https://github.com/user-attachments/assets/1ee5d8b2-9182-48bf-88f1-8f6750800718)

Шаг 8. 
- в первой сессии добавить новую запись
  insert into persons(first_name, second_name) values('sergey', 'sergeev');
- сделать select from persons во второй сессии
![image](https://github.com/user-attachments/assets/4aa60809-77a7-4a1b-acaa-6bfac38ae124)

Видите ли вы новую записьво второй сессии и если да то почему?
- Нет, новая запись не видна, в таблице так и осталось 2 строки.
  Как видели на скрине выше, имеем уровень изоляции Read Committed. Он гарантирует, что транзакция видит только зафиксированные изменения других транзакций

Шаг 9.
- завершить первую транзакцию
  commit;
- сделать select * from persons во второй сессии
![image](https://github.com/user-attachments/assets/4879d470-2b5d-413f-b890-f0cff0428124)

Видите ли вы новую запись и если да то почему?
- Да, новая запись видна, т.к. мы зафиксировали изменения, внесенные первой сессией.

Шаг 10. Начать новые но уже repeatable read транзации
    set transaction isolation level repeatable read;
![image](https://github.com/user-attachments/assets/13ebf105-a7a3-4e3e-ac0c-8ce0e883a156)

Шаг 11. 
- в первой сессии добавить новую запись
  insert into persons(first_name, second_name) values('sveta', 'svetova');
- сделать select * from persons во второй сессии
![image](https://github.com/user-attachments/assets/5a853043-ae19-4255-bc23-6724aad071cb)

Видите ли вы новую запись и если да то почему?
- Нет, новая запись не видна, в таблице так и отобраается 3 строки.

Шаг 12.
- завершить первую транзакцию
  commit;
- сделать select from persons во второй сессии
![image](https://github.com/user-attachments/assets/6551c5da-1a5b-46db-9c47-8f13866da7ba)

Видите ли вы новую запись и если да то почему?
- Да, новая запись видна, т.к. мы зафиксировали изменения, внесенные первой сессией.

Шаг 13.
- завершить вторую транзакцию
- сделать select * from persons во второй сессии
![image](https://github.com/user-attachments/assets/f313c3af-eca2-4e4f-86d3-3eae867bc05d)

Видите ли вы новую запись и если да то почему?
- Да, новая запись видна, т.к. мы зафиксировали изменения, внесенные первой сессией.
