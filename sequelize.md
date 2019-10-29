
# sequelize

## Tags
* nodejs
* bd

## Links
> [https://sequelize.org](https://sequelize.org)
> https://metanit.com/web/nodejs/9.2.php

## Notes

#### Создание сущности в бд (1 вариант) 
```js
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

#### Создание сущности в бд (2 вариант)
```js
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

####  Синхронизация с бд
Параметры
1) {force: true} - удалить сущность и создать заного
```js
sequelize.sync(?параметр).then((result) => ...).catch((err)=> ...);
```
#### Добавить сущность
```js
User.create({name: myName, age: 30}).then((data)=> ...).catch((err)=> ...)
```

#### Получить все данные по сущностям User в виде объекта
```js
User.findAll({raw: true }).then((data)=> ...).catch((err)=> ...)
```

#### Получить сущность по номеру
```js
User.findByPk(2).then((data)=> ...).catch((err)=> ...)
```

#### Получить сущность по имени
```js
User.findAll({where:{name: "Tom"}, raw: true }).then((data)=> ...).catch((err)=> ...)
```

####  Обновить свойства age у всех объектов с именем myName
```js
User.update({ age: 36 }, {where: {name: myName}}).then((data)=> ...).catch((err)=> ...)
```

#### Удалить сущность c именем myName
```js
User.destroy({where: {name: myName}}).then((data)=> ...).catch((err)=> ...)
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE0MzIzMjEwNDddfQ==
-->