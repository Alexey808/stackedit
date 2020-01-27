# Base
Полезные ссылки: [https://habr.com/ru/post/351890/](https://habr.com/ru/post/351890/)  

-   **GET**:  этот метод является безопасным и идемпотентным. Обычно используется для извлечения информации и не имеет побочных эффектов.
-   **POST**:  этот метод не является ни безопасным, ни идемпотентным. Этот метод наиболее широко используется для создания ресурсов.
-   **PUT**:  этот метод является идемпотентным. Вот почему лучше использовать этот метод вместо POST для обновления ресурсов. Избегайте использования POST для обновления ресурсов.
-   **DELETE**:  как следует из названия, этот метод используется для удаления ресурсов. Но этот метод не является идемпотентным для всех запросов.
-   **OPTIONS**:  этот метод не используется для каких-либо манипуляций с ресурсами. Но он полезен, когда клиент не знает других методов, поддерживаемых для ресурса, и используя этот метод, клиент может получить различное представление ресурса.
-   **HEAD**:  этот метод используется для запроса ресурса c сервера. Он очень похож на метод GET, но HEAD должен отправлять запрос и получать ответ только в заголовке. Согласно спецификации HTTP, этот метод не должен использовать тело для запроса и ответа.

## Коды статуса ответа HTTP

Информационные ответы (100–199)
Успешные ответы (200–299)
Перенаправления (300–399)
Ошибки клиента (400–499)
Ошибки сервера (500–599)

# Nestjs example API

```ts
import { Body, Controller, Delete, Get, Post, Param, Query, Put } from '@nestjs/common';  
import { UsersService } from './users.service';  
import { UserDTO } from './dto/create-user.dto';  
  
@Controller('api/users')  
export class UsersController {  
  constructor(  
    private readonly usersService: UsersService,  
  ) {}  
  
  // ..api/users/1
  @Get(':id')  
  async getUser(@Param('userId') userId) {  
    return await this.usersService.getUser(userId);  
  }  
  
  // ..api/users
  @Get()  
  async getUsers() {  
    return await this.usersService.getUsers();  
  }  
  
  // ..api/users (остальное в body)
  @Post()  
  async addUser(@Body() createUserDTO: UserDTO) {  
    return await this.usersService.addUser(createUserDTO);  
  }  
  
  // ..api/users?userId=1
  /* *
   * Думаю другой ниже метод правильней, так как с "userId"
   * а не просто "id" он превращается в query param.  
   * С другой стороны можно было обойтись просто парамом с "id"    
   * */
  // @Delete('/:userId')  
  // async deleteUser(@Param('id') id: string) {  
  //   return await this.usersService.deleteUser(id);  
  // }  
  
  // ..api/users?id=1
  @Delete()  
  async deleteUser(@Query() query) { 
    return await this.usersService.deleteUser(query.id); 
  } 
  
  // ..api/users/1 (остальное в body)
  @Put(':id')  
  async updateUser(@Param('id') id: string, @Body()   updateUserDTO: UserDTO) {  
    return await this.usersService.updateUser(id, updateUserDTO);  
  }

}
```


<!--stackedit_data:
eyJoaXN0b3J5IjpbMzUwNjc2MDg0LC0zNTkyNTUxMTAsLTk3Mj
Q4NTE2MCwxMjgwMDc4NjI3XX0=
-->