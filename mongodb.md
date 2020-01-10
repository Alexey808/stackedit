## README - MongoDB

`sudo service mongod start`  
`sudo service mongod status`  
`sudo service mongod stop`  
`sudo service mongod restart`  
`mongo` - запуск оболочки  

`show dbs` - просмотр всех бд  
`use NAME_DATABASE` - выбрать бд  
`show collection` - просмотр коллекций  
`db.users.find()` - вывод коллекции users  
`db.users.insertOne({name: 'test'})` - добавление сущности
`db.users.deleteOne({id: 3})` - удаление пользователя с id = 3  
`db.users.remove({})` - удалить все сущности users  
`db.users.updateOne({id: 3}, {$set: {"role":"admin"}}, false, true)` - обновление сущности  
`db.sprintDayEntity.find({spDeferred: {$ne: null}})` - поиск сущности по полю  

**Зайти в БД внутрь докер контейнера где докерскую бд смотреть через docker ps**  
```
docker exec -it 5e61ca6761d1 /bin/bash
```
**Распаковка бэкапа**  
Если расположение распакованной бд след   `~/develop/work/test/mongo/dump/testing`
```
sudo mongorestore --db testing_plan ~/develop/work/test/mongo/dump/testing/
```
**Удаление пакетов MongoDB**  
```
sudo apt-get purge mongodb-org*
```
**Удаление баз данных**  
```
sudo rm -r /var/log/mongodb
sudo rm -r /var/lib/mongodb
```





<!--stackedit_data:
eyJoaXN0b3J5IjpbNDczMTMxNjUwLC0xMjk3NTAxMzEyLC0xOT
UwMjM4MzU2LC01MDY1NjYxNDYsLTE1NDc4NzgxNTYsNDk3ODE4
ODEwLDEyODk2MTI0MjddfQ==
-->