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
   * а не просто "id" он превращается в query param? 
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
  
  // ..api/users?1 (остальное в body)
  @Put(':id')  
  async updateUser(@Param('id') id: string, @Body()   updateUserDTO: UserDTO) {  
    return await this.usersService.updateUser(id, updateUserDTO);  
  }

}
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTI4MDA3ODYyN119
-->