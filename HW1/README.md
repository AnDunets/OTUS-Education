#HW - Установка и настройка PostgteSQL

Цель:
- установить PostgreSQL в Docker контейнере
- настроить контейнер для внешнего подключения

Шаг 1. Создать ВМ с Ubuntu 20.04/22.04 или развернуть докер любым удобным способом

Ключ был создан в приложении PuTTYgen.
Виртуальная машина была создана в ЯО, подключение к ней производилось через приложение PuTTY.

Шаг 2. Поставить PostgreSQL
Для установки PostgreSQL на ВМ применялась команда:
    sudo apt install postgresql
![image](https://github.com/user-attachments/assets/10b8240b-d4bf-4fc2-933c-f814503ebae3)

Шаг 3. Получить параметры кластера
     sudo pg_lsclusters
![image](https://github.com/user-attachments/assets/c6bbba90-7811-43d1-951f-a30e913b95ef)

Шаг 4. Подключение к БД под пользователем postgres
     sudo -u postgres psql
![image](https://github.com/user-attachments/assets/5abd5fea-b69c-45b5-b4b2-79d722d1a3cd)
