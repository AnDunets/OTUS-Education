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

Шаг 6. Создание нового диска размером 10GB
![image](https://github.com/user-attachments/assets/c9178a32-79f0-456c-89fd-0dfc89417f50)

Шаг 7. Добавление свеже-созданного диска к виртуальной машине
![image](https://github.com/user-attachments/assets/d07c056a-5e88-420e-b9d1-44a65c3d3465)
![image](https://github.com/user-attachments/assets/1ca04ef9-a305-4db5-95f9-eacf48d5be78)

Шаг 8. Инициализация диска согласно инструкции и подмонтирование файловой системы
  sudo apt update
  sudo apt install parted
  sudo parted -l | grep
![image](https://github.com/user-attachments/assets/f2a104dd-c2ca-4149-b76a-9246bd69c005)
  lsblk
![image](https://github.com/user-attachments/assets/48ca397a-2383-41c6-9cd1-2fd0ea1927a5)
  sudo parted /dev/vdb mklabel gpt
  sudo parted -a opt /dev/vdb mkpart primary ext4 0% 100%
  lsblk
![image](https://github.com/user-attachments/assets/97a52357-864c-4916-b148-7dd0b42e3dfe)
  sudo mkfs.ext4 -L datapartition /dev/vdb1
  sudo lsblk --fs
![image](https://github.com/user-attachments/assets/6c6714df-4038-4fad-9c05-4df573eccf54)
  sudo mkdir -p /mnt/data
  sudo mount -o defaults /dev/vdb1 /mnt/data
  sudo nano /etc/fstab
  sudo mount -a
  df -h
![image](https://github.com/user-attachments/assets/4779af8a-9b82-4b4e-9833-80a2950a5dae)

Шаг 9. Перезагрузить инстанс
После перезагрузки инстанса диск не остался примонтированным
![image](https://github.com/user-attachments/assets/f622449a-3fe1-473e-b093-dc67f9ad7b5e)
Решение:
![image](https://github.com/user-attachments/assets/64d1ff99-8eb8-4eeb-b96e-3f126988b9ca)
Теперь после перезагрузки диск не исчез
![image](https://github.com/user-attachments/assets/799260d2-6a8a-46dd-885c-17bf96e24f7b)

Шаг 10. Сделать пользователя postgres владельцем /mnt/data
   sudo chown -R postgres:postgres /mnt/data/
![image](https://github.com/user-attachments/assets/9438ff67-8e55-4de7-8478-33fcac8ff2e9)

Шаг 11. Перенести содержимое /var/lib/postgres/17 в /mnt/data
![image](https://github.com/user-attachments/assets/ca81599e-2a27-46bd-ab65-a52a93bed7c1)

Шаг 12. Запуск кластера
При вызове команды sudo -u postgres pg_ctlcluster 17 main start получаем ошибку, т.к. изменили место расположения файла. Необхоимо изменить путь в конфигурационном файле
![image](https://github.com/user-attachments/assets/cc04ae6e-d96a-48ab-924b-20cefc507aae)

Шаг 13. Найти конфигурационный параметр в файлах раположенных в /etc/postgresql/17/main, который надо поменять, и поменяйте его
Заходим в нужную директорию и смотрим ее содержимое
![image](https://github.com/user-attachments/assets/0baf86e5-ceb6-45bf-a733-c52dd90aaf9d)
Открываем файл (sudo nano postgresql.conf) и редактируем путь:
  Было
  ![image](https://github.com/user-attachments/assets/957f2a5c-5eaa-48e4-b12b-a2926f3304a5)
  Стало
  ![image](https://github.com/user-attachments/assets/bf61f7ca-5893-474b-a6d3-0c81db7ee803)

Шаг 15. Запуск кластера
  sudo -u postgres pg_ctlcluster 17 main start
  sudo -u postgres pg_lsclusters
  ![image](https://github.com/user-attachments/assets/0eeac964-e737-42c6-a2d7-a9a20d8f7ce1)


