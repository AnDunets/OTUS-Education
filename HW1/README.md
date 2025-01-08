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
![image](https://github.com/user-attachments/assets/a2af8630-dba9-4105-a7e4-0c3018eba750)

Шаг 5. Выключить auto commit
![image](https://github.com/user-attachments/assets/cf7be723-616d-4d28-b169-1bf4009a50ec)

Шаг 6. В первой сессии новую таблицу и наполнить ее данными 
    create table persons(id serial, first_name text, second_name text); 
    insert into persons(first_name, second_name) values('ivan', 'ivanov'); 
    insert into persons(first_name, second_name) values('petr', 'petrov'); 
    commit;
    ![image](https://github.com/user-attachments/assets/ac9b1b67-320f-4ab4-acef-d4c05a745cc1)
