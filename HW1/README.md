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

