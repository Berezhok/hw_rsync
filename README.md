## Домашнее задание к занятию 3 «Резервное копирование»

## Задание 1
### Составьте команду rsync, которая позволяет создавать зеркальную копию домашней директории пользователя в директорию /tmp/backup
### Необходимо исключить из синхронизации все директории, начинающиеся с точки (скрытые)
### Необходимо сделать так, чтобы rsync подсчитывал хэш-суммы для всех файлов, даже если их время модификации и размер идентичны в источнике и приемнике.
### На проверку направить скриншот с командой и результатом ее выполнения
## Решение
### Была проведена синхронизация и создание копии файлов с локальной машины на виртуальную машину в облаке по SSH
### ИСпользовалась данная команда : rsync -acP --exclude "/.*" --exclude "*.deb" --exclude "/snap/*" /home/berezhok/ rsinc_test@158.160.83.197:/tmp/test
### ![](https://github.com/Berezhok/hw_rsync/blob/main/img/comand_rsync.png)
### На удаленной машине файлы появились за исключением скрытых файлов и архивов, также исключил всю директорию /snap
### ![](https://github.com/Berezhok/hw_rsync/blob/main/img/cloud_server.png)
### Вроде что-то получилось

## Задание 2
### Написать скрипт и настроить задачу на регулярное резервное копирование домашней директории пользователя с помощью rsync и cron.
### Резервная копия должна быть полностью зеркальной
### Резервная копия должна создаваться раз в день, в системном логе должна появляться запись об успешном или неуспешном выполнении операции
### Резервная копия размещается локально, в директории /tmp/backup
### На проверку направить файл crontab и скриншот с результатом работы утилиты.

## Решение
### Написали bash-скрипт, который создает копию файлов локально в /tmp/backup и записью в log-файл об успешном или неудачном выполнении задачи и времени
### исполнения.
### ![](https://github.com/Berezhok/hw_rsync/blob/main/img/bash.png)
### Создали crontab файл, который запускает скрипт каждый день в 11 часов 10 минут
### 10 11 * * * bash /home/berezhok/cron_backUp.sh
### ![](https://github.com/Berezhok/hw_rsync/blob/main/img/crontab_e.png)
### Вроде работает. Файлы скопировались. Запись в log записалась об успешном копировании. 
### ![](https://github.com/Berezhok/hw_rsync/blob/main/img/result.png)
### При этом правильно срабатывает только при запуске crontab -e только через sudo. Если запускать без sudo , копирование не произойдет и в log-файл 
### пойдет сообщение об неуспешной операции.  
###
