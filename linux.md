**Установка deb пакетов**  
`sudo dpkg -i имя_пакета.deb`

**
```
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
eyJoaXN0b3J5IjpbLTExNTY1ODIzNjUsMjk1MjA0ODQsNzUzMz
M0MzcyXX0=
-->