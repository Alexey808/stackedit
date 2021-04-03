**Установка deb пакетов**  
`sudo dpkg -i имя_пакета.deb`

## Наброски _daemon_ (фоновых процессов
**
```bash
#!/bin/bash

echo Hello!!!111!!!!

gnome-terminal
#setxkbmap us

#/usr/systemd/system/test-daemon.service
#/home/alexey/scripts/test-daemon-service.sh

#sudo chmod +x /home/alexey/scripts/test-daemon-service.sh
#sudo systemctl start test-daemon.service
#sudo systemctl stop test-daemon.service
#sudo systemctl status test-daemon.service
```
**
```bash
[Unit]
Description=TEST-DEMON

# тест комментария на русском
[Service]
RemainAfterExit=true
ExecStart=/home/alexey/alexey/init/test-demon-start.service
Type=oneshot

[Install]
WantedBy=multi-user.target
```
**
```bash
### Команды

# sudo systemctl enable НАЗВАНИЕ_ДЕМОНА - включить в автозагрузку
# sudo systemctl start НАЗВАНИЕ_ДЕМОНА - запустить
# sudo systemctl stop НАЗВАНИЕ_ДЕМОНА
# sudo systemctl status НАЗВАНИЕ_ДЕМОНА
# sudo systemctl daemon-reload
# journalctl -u НАЗВАНИЕ_ДЕМОНА - логи


### Дополнительные сведенья

# сам демон должен лежать в /etc/systemd/system/НАЗВАНИЕ_ДЕМОНА
# /usr/local/bin/НАЗВАНИЕ_СКРИПТА			test-script-for-demon.sh

### Сервис
[Unit]

# Описание
Description=TEST-DEMON
[Service]

# Оставляем процесс висеть после его выполнения
RemainAfterExit=true

# Указывает скрипт выполнить перед остановкой сеанса
# ExecStop=/usr/local/bin/test-demon-end.service

# Указывает скрипт выполнить при старте демона
ExecStat=/usr/local/bin/test-demon-start.service

# Тип сервиса, oneshot - разовое выполнение
Type=oneshot


[Install]

# Запуск при загрузке системы
WantedBy=multi-user.target
```


<!--stackedit_data:
eyJoaXN0b3J5IjpbMTI1NjEyNTI5OCwxNzUyNzIxOTE3LDI5NT
IwNDg0LDc1MzMzNDM3Ml19
-->