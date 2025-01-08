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


