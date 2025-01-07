#HW - Установка и настройка PostgreSQL

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
![image](https://github.com/user-attachments/assets/4583a19d-f1a9-49d3-855e-c3bd1132ad95)
![image](https://github.com/user-attachments/assets/863a83c7-372e-4694-828b-845b2a8b9819)

Шаг 5. Развернуть контейнер с клиентом postgres
   sudo docker run -it --rm --network posgtres-net --name pg-client postgres:16 psql -h (Внутренний IPv4-адрес ВМ) -U postgres

Шаг 6. Создать БД
![image](https://github.com/user-attachments/assets/f91bb609-1c6a-455c-9d96-d3f859b83d14)
![image](https://github.com/user-attachments/assets/8ccc73a4-1c71-435a-b3b9-09d47c32795b)

Шаг 7. Сделать таблицу с парой строк
![image](https://github.com/user-attachments/assets/6ac74b68-029d-4952-a828-4ef953e1a506)

Шаг 8. Подключится к контейнеру с сервером с ноутбука/компьютера извне инстансов ЯО/места установки докера
![image](https://github.com/user-attachments/assets/804f08f1-5347-4d24-8448-d3685eb2164f)

Шаг 9. Удалить контейнер с сервером
![image](https://github.com/user-attachments/assets/aa3c3c61-5802-497d-aec3-43e936bbc0ae)
   sudo docker rm 936873ee08a4

Шаг 10. Создать его заново
![image](https://github.com/user-attachments/assets/c7bfaa93-93bd-4bc3-84b9-9b8c8aecf647)

Шаг 11. Подключиться снова из контейнера с клиентом к контейнеру с сервером
![image](https://github.com/user-attachments/assets/02bfec7a-798b-41b4-bfc8-70bd444f5f4a)

Шаг 12. Проверить, что данные остались на месте
![image](https://github.com/user-attachments/assets/9d601286-4735-4c07-9b3e-df461e23620c)
![image](https://github.com/user-attachments/assets/94843992-2e23-416f-a076-b9c1b38cf672)
