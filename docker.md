
# Docker

## Links
https://habr.com/ru/post/309556/  

```docker
FROM ubuntu:16.04 # наследуемый образ  
COPY ./ /app # копирование файлов куда пробел что  
WORKDIR /app # рабочая директория  
RUN apt update && apt install nano # команды доступные благодаря наследуемому образу  
ENTRYPOINT [“/app/tomcat/catalina.sh”]  # запускать исполняемый файл каждый раз при старте
```

**Удалить image**  
`docker rmi image_name:tag`

**Удалить все images**  
`docker rmi $(docker images -a -q)`

**Удалить container**  
`docker rm id_или_name`

**Удалить все контейнеры**  
`docker rm -f $(docker ps -a -q)`

**Контейнер (закрываемый вместе с процессом)**  
`docker run -ti ...`

**Список контейнеров**  
`docker ps`

**Список имеджей**  
`docker images`

**Основная очистка**  
`docker system prune`

**Очищаем volume (если не создавали вручную проблем быть не должно)**  
`docker volume prune`

**Удаляем все image страше 3 месяцeв**  
`docker image prune -a --filter "until=2160h"`

**Проверка нагрузки на контейнеры**  
`docker stats $(docker inspect -f '{{.Name}}' $(docker ps -q) | cut -c 2-)`

**Перезапуск одного сервиса в compose | compose**  
`docker-compose up -d --force-recreate --no-deps SERVICE_NAME`

**Раздача прав для запуска sh | linux**  
`sudo chown -R $(whoami) /usr/local/bin`

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEwNzAwNjM4NTksMjA5NzA2MzExNywxND
IxODA2MDRdfQ==
-->