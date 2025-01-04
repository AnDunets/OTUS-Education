#HW - Установка и настройка PostgteSQL

Цель:
- установить PostgreSQL в Docker контейнере
- настроить контейнер для внешнего подключения

Шаг 1. Создать ВМ с Ubuntu 20.04/22.04 или развернуть докер любым удобным способом
Ключ был создан в приложении PuTTYgen. Виртуальная машина была создана в ЯО, подключение к ней производилось через приложение PuTTY.

Шаг 2. Поставить на нем Docker Engine
Для установки Docker Engine использовалась инструкция с сайта: https://docs.docker.com/engine/install/ubuntu/
![image](https://github.com/user-attachments/assets/484cb9db-6a02-4a2c-afc5-a8abe9754d37)

Шаг 3. Сделать каталог /var/lib/postgres
![image](https://github.com/user-attachments/assets/f1da250e-e380-4d31-8580-c88b43e0a78f)

Шаг 4. Развернуть контейнер с PostgreSQL смонтировав в него /var/lib/postgresql
![image](https://github.com/user-attachments/assets/92a20630-5384-478e-b352-1fd4de779b47)
![image](https://github.com/user-attachments/assets/73d11846-beb5-499f-a5c4-b3afbe4ba095)

Шаг 5. Развернуть контейнер с клиентом postgres
