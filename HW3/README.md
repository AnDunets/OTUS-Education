#HW - Установка и настройка PostgreSQL

Цель:
- создавать дополнительный диск для уже существующей виртуальной машины, размечать его и делать на нем файловую систему
- переносить содержимое базы данных PostgreSQL на дополнительный диск
- переносить содержимое БД PostgreSQL между виртуальными машинами

Шаг 1. Создать ВМ с Ubuntu 20.04/22.04 или развернуть докер любым удобным способом
Ключ был создан в приложении PuTTYgen. Виртуальная машина была создана в ЯО, подключение к ней производилось через приложение PuTTY.

Шаг 2. Поставить PostgreSQL 
Для установки PostgreSQL на ВМ применялась команда: sudo apt install postgresql

Шаг 3. Проверить, что кластер запущен
![image](https://github.com/user-attachments/assets/3423884b-814b-46ef-9dc8-8c8522d8d152)

Шаг 4. Зайти из под пользователя postgres в psql и сделать произвольную таблицу с произвольным содержимым
  sudo -u postgres psql
  create table test(c1 text);
  insert into test values('1');
  \q
![image](https://github.com/user-attachments/assets/c689c6c3-bc16-484d-946a-4f4eab2f6bf9)

Шаг 5. Остановить postgres
 sudo systemctl stop postgresql@17-main
![image](https://github.com/user-attachments/assets/83dec9a3-25aa-40a4-89a6-eeb428ff5bdb)
