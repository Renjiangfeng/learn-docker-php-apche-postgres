### 运行

1. 检查 docker-compose 中的端口，避免与本地的冲突
2. 执行 `docker-compose up` 启动相关容器

### 注意

1. 如果修改了某一 dockerfile 后要重建镜像
`docker-compose build --no-cache`
2. 关于PHP，默认是7.0.1，如果需要安装其他版本，修改php/Dockerfile中的第一行
FROM php:x.x.x-fpm
3. 关于MySQL连接配置
宿主机连接MySQL，host为localhost，端口默认33060。
项目代码中连接，host填写mysql(容器名，docker会自动转换)或docker中的IP，端口3306。
4. 如果是Laravel项目，执行php artisan。 使用 `docker-compose exec <php-container> php artisan`
https://github.com/laradock/laradock/issues/610
5. 不重启容器重启加载php.ini。 `docker exec -it <php-container> kill -USR2 1`
https://github.com/docker-library/php/issues/399


> IP具体查看方法：

查看容器详情
`docker inspect <mysql-container>`
找到 IPAddress
或者进入容器 `docker exec -it <mysql-container> bash`，执行
 `/sbin/ip route|awk '/default/ { print $3 }'`