Настройка репликации происходит в несколько шагов. Мы будем использовать два сервера с адресами:

    Master сервер, 10.10.0.1
    Slave сервер, 10.10.0.2

## Шаг 1. Настройка Мастера

На сервере, который будет выступать мастером, необходимо внести правки в my.cnf:
```
# выбираем ID сервера, произвольное число, лучше начинать с 1
server-id = 1
# путь к бинарному логу
log_bin = /var/log/mysql/mysql-bin.log
# название Вашей базы данных, которая будет реплицироваться
binlog_do_db = newdatabase
```

Перезапускаем Mysql:

```
/etc/init.d/mysql restart
```

## Шаг 2. Права на репликацию

Далее необходимо создать профиль пользователя, из под которого будет происходить репликация. Для этого запускаем консоль:

```
mysql -u root -p
```

Далее создаем и назначаем права пользователю для реплики:

```
GRANT REPLICATION SLAVE ON *.* TO 'slave_user'@'%' IDENTIFIED BY 'password';
FLUSH PRIVILEGES;
```

даем права пользователю slave_user с паролем password

Далее блокируем все таблицы в нашей базе данных:

```
USE newdatabase;
FLUSH TABLES WITH READ LOCK;
Проверяем статус Мастер-сервера:
SHOW MASTER STATUS;
```

Мы увидим что-то похожее на:

```
mysql> SHOW MASTER STATUS;
+------------------+----------+--------------+------------------+ 
| File | Position | Binlog_Do_DB | Binlog_Ignore_DB |
+------------------+----------+--------------+------------------+ 
**mysql-bin.000001** | **107** | newdatabase | 
+------------------+----------+--------------+------------------+ 
1 row in set (0.00 sec)
```
Выделенные значения мы будем использовать для запуска Слейва

## Шаг 3. Дамп базы

Теперь необходимо сделать дамп базы данных:

```
mysqldump -u root -p newdatabase > newdatabase.sql
```

Разблокируем таблицы в консоли mysql:

```
UNLOCK TABLES;
```

## Шаг 4. Создание базы на слейве

В консоли mysql на Слейве создаем базу с таким же именем, как и на Мастере:
```
CREATE DATABASE newdatabase;
```

После этого загружаем дамп (из bash):
```
mysql -u root -p newdatabase < newdatabase.sql
```

## Шаг 5. Настройка Слейва

В настройках my.cnf на Слейве необходимо указать такие параметры:

```
# ID Слейва, удобно выбирать следующим числом после Мастера
server-id = 2
# Путь к relay логу
relay-log = /var/log/mysql/mysql-relay-bin.log
# Путь к bin логу на Мастере
log_bin = /var/log/mysql/mysql-bin.log
# База данных для репликации
binlog_do_db = newdatabase
```

## Шаг 6. Запуск Слейва

Нам осталось включить репликацию, для этого необходимо указать параметры подключения к мастеру. В консоли mysql на Слейве необходимо выполнить запрос:

```
CHANGE MASTER TO MASTER_HOST='10.10.0.1', MASTER_USER='slave_user', MASTER_PASSWORD='password',
MASTER_LOG_FILE = 'mysql-bin.000001', MASTER_LOG_POS = 107;
##Указанные значения мы берем из настроек Мастера
После этого запускаем репликацию на Слейве:
START SLAVE;
```

Статус репликации

Проверить работу репликации на Слейве можно запросом:

```
mysql> SHOW SLAVE STATUS
             Slave_IO_State: Waiting for master to send event
                Master_Host: localhost
                Master_User: root
                Master_Port: 3306
              Connect_Retry: 3
            Master_Log_File: gbichot-bin.005
        Read_Master_Log_Pos: 79
             Relay_Log_File: gbichot-relay-bin.005
              Relay_Log_Pos: 548
      Relay_Master_Log_File: gbichot-bin.005
           Slave_IO_Running: Yes
          Slave_SQL_Running: Yes
            Replicate_Do_DB:
        Replicate_Ignore_DB:
         Replicate_Do_Table:
     Replicate_Ignore_Table:
    Replicate_Wild_Do_Table:
Replicate_Wild_Ignore_Table:
                 Last_Errno: 0
                 Last_Error:
               Skip_Counter: 0
        Exec_Master_Log_Pos: 79
            Relay_Log_Space: 552
            Until_Condition: None
             Until_Log_File:
              Until_Log_Pos: 0
         Master_SSL_Allowed: No
         Master_SSL_CA_File:
         Master_SSL_CA_Path:
            Master_SSL_Cert:
          Master_SSL_Cipher:
             Master_SSL_Key:
      Seconds_Behind_Master: 8
```
