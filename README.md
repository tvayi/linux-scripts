1. Создаем скрипт и запускаем его в фоновом режиме

```bash
sudo touch /opt/script.sh
sudo chmod +x /opt/script.sh
echo 'while true; do date >> /opt/my.log; sleep 1; done' | sudo tee /opt/script.sh
```

2. Создаем скрипт в фоновом режиме

```bash
sudo nohup /opt/script.sh &
```

3. Удаляем скрипт

sudo rm /opt/script.sh

4. Проверяем, что скрипт работает в фоновом режиме

```bash
tail -f /opt/my.log
```

5. Запускаем команду 

```bash
tail -f /opt/my.log
```

Видим, что процесс с PID 2147 пишет в файл /opt/my.log


6. Смотрим файловые дескрипторы процесса

```bash
sudo   ls -l /proc/2146/fd
```

Видим следующий аутпут

```bash
total 0
l-wx------ 1 root root 64 Mar  5 01:50 0 -> /dev/null
l-wx------ 1 root root 64 Mar  5 01:50 1 -> /home/student/nohup.out
lr-x------ 1 root root 64 Mar  5 02:00 10 -> '/opt/script.sh (deleted)'
l-wx------ 1 root root 64 Mar  5 01:50 2 -> /home/student/nohup.out
```

7. Видим, что дескриптор 10 указывает на удаленный файл. Проверяем, что там находится

```bash
sudo cat /proc/2147/fd/10
```

Видим удаленный скрипт после выполнения команды

```bash
while true; do date >> /opt/my.log; sleep 1; done
```
