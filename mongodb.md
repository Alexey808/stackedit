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
`db.users.deleteOne({id: 3})` - удаление пользователя с id = 3  
`db.users.remove({})` - удалить все сущности users  
 

`db.users.updateOne({id: 3}, {$set: {"role":"admin"}}, false, true)` - обновление сущности  

**Распаковка бэкапа**
Если расположение распакованной бд след   `~/develop/work/test/mongo/dump/testing`
```
sudo mongorestore --db testing_plan ~/develop/work/test/mongo/dump/testing/
```
**Удаление пакетов Mongodb**  
```
sudo apt-get purge mongodb-org*
```
**Удаление баз данных**  
```
sudo rm -r /var/log/mongodb
sudo rm -r /var/lib/mongodb
```





<!--stackedit_data:
eyJoaXN0b3J5IjpbMjA2MDg4MjMxMCwtMTk1MDIzODM1NiwtNT
A2NTY2MTQ2LC0xNTQ3ODc4MTU2LDQ5NzgxODgxMCwxMjg5NjEy
NDI3XX0=
-->