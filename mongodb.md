## Начало работы в БД
`sudo service mongod start`
`sudo service mongod status`
`sudo service mongod stop`
`sudo service mongod restart`
`mongo` - запуск оболочки

**Удаление пакетов Mongodb**  
```
sudo apt-get purge mongodb-org*
```
**Удаление баз данных**  
```
sudo rm -r /var/log/mongodb
sudo rm -r /var/lib/mongodb
```

##

**Создание сущности в бд (1 вариант)**  
```
const User = sequelize.define("user", {
  id: {
    type: Sequelize.INTEGER,
    autoIncrement: true,
    primaryKey: true,
    allowNull: false
  },
  name: {
    type: Sequelize.STRING,
    allowNull: false
  },
  age: {
    type: Sequelize.INTEGER,
    allowNull: false
  }
});
```
**Создание сущности в бд (2 вариант)**  
```
class User extends Model {}
User.init({
  id: {
    type: Sequelize.INTEGER,
    autoIncrement: true,
    primaryKey: true,
    allowNull: false
  },
  name: {
    type: Sequelize.STRING,
    allowNull: false
  },
  age: {
    type: Sequelize.INTEGER,
    allowNull: false
  }
}, {
  sequelize,
  modelName: "user"
});
```
**Синхронизация с бд**  
{force: true} - удалить сущность и создать заного  
`sequelize.sync(параметр).then((result) => ...).catch((err)=> ...);`

**Добавить сущность**  
`User.create({name: myName, age: 30}).then((data)=> ...).catch((err)=> ...)`

**Получить все данные по сущностям User в виде объекта**  
`User.findAll({raw: true }).then((data)=> ...).catch((err)=> ...)`

**Получить сущность по номеру**  
`User.findByPk(2).then((data)=> ...).catch((err)=> ...)`

**Получить сущность по имени**  
`User.findAll({where:{name: "Tom"}, raw: true }).then((data)=> ...).catch((err)=> ...)`

**Обновить свойства age у всех объектов с именем myName**  
`User.update({ age: 36 }, {where: {name: myName}}).then((data)=> ...).catch((err)=> ...)`

**Удалить сущность c именем myName**  
`User.destroy({where: {name: myName}}).then((data)=> ...).catch((err)=> ...)`
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTM0OTI4MzU0MSwtNTA2NTY2MTQ2LC0xNT
Q3ODc4MTU2LDQ5NzgxODgxMCwxMjg5NjEyNDI3XX0=
-->