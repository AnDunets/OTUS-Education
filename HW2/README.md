#HW - Установка и настройка PostgteSQL

Цель:
- установить PostgreSQL в Docker контейнере
- настроить контейнер для внешнего подключения

Шаг 1. Создать ВМ с Ubuntu 20.04/22.04 или развернуть докер любым удобным способом
Ключ был создан в приложении PuTTYgen. Виртуальная машина была создана в ЯО, подключение к ней производилось через приложение PuTTY.

Шаг 2. Поставить на нем Docker Engine
Для установки Docker Engine использовалась инструкция с сайта: https://docs.docker.com/engine/install/ubuntu/
![image](https://github.com/user-attachments/assets/babea19e-d223-4406-8776-a96444668fbe)

Шаг 3. Сделать каталог /var/lib/postgres
![image](https://github.com/user-attachments/assets/f1da250e-e380-4d31-8580-c88b43e0a78f)

Шаг 4. Развернуть контейнер с PostgreSQL смонтировав в него /var/lib/postgresql
![image](https://github.com/user-attachments/assets/9d814f03-1c6b-494f-adad-63c7d7f35083)

Шаг 5. Развернуть контейнер с клиентом postgres
  sudo docker run -it --rm --name pg-client postgres:16 psql -h 5432 -U postgres
![image](https://github.com/user-attachments/assets/ed6b27d9-4f68-46d2-959e-ae5e82a739ce)

