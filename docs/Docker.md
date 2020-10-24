### Docker

#### Docker 安装 MySQL 并挂载文件

- docker 命令

```
docker run -i -t --name mysql --restart=always --privileged=true -e MYSQL_ROOT_PASSWORD=数据库密码 -p 3306:3306 \ 
-v /data/mysql/data:/var/lib/mysql \
-v /data/mysql/cnf:/etc/mysql/conf.d \
-v /data/mysql/logs:/var/log/mysql -d mysql \
--character-set-server=utf8mb4 --collation-server=utf8mb4_unicode_ci
```


- my.cnf 配置 修改默认的 sql_mode

```
[mysqld]
sql_mode = 'STRICT_TRANS_TABLES,NO_ZERO_IN_DATE,NO_ZERO_DATE,ERROR_FOR_DIVISION_BY_ZERO,NO_ENGINE_SUBSTITUTION'
max_connections = 512
```

#### Docker 安装 Nginx  

- docker 命令

```
docker run -i -t --name nginx --restart=always --privileged=true -d -p 80:80 -p 443:443 \
-v /data/nginx/conf/nginx.conf:/etc/nginx/nginx.conf \
-v /data/nginx/log:/var/log/nginx \
-v /data/nginx/html:/usr/share/nginx/html \
-v /data/nginx/conf.d:/etc/nginx/conf.d nginx \
-v /data/nginx/cert:/etc/nginx/cer
```

#### Docker 安装 redis 

- docker 命令
```
docker run -d -- name redis --restart=always --privileged=true \
-p 6379:6379 --restart always -v /data/redis/conf/redis.conf:/etc/redis/redis.conf \
-v /data/redis/data:/data redis-server /etc/redis/redis.conf --appendonly yes
```



#### 命令介绍
```textmate
-d                                                              -> 以守护进程的方式启动容器
-p 6379:6379                                                    -> 绑定宿主机端口
--name myredis                                                  -> 指定容器名称
--restart always                                                -> 开机启动
--privileged=true                                               -> 提升容器内权限
-v /root/docker/redis/conf:/etc/redis/redis.conf                -> 映射配置文件
-v /root/docker/redis/data:/data                                -> 映射数据目录
--appendonly yes                                                -> 开启数据持久化
--character-set-server=utf8mb4                                  -> MySQL编码格式
--collation-server=utf8mb4_unicode_ci                           -> MySQL编码格式
-e MYSQL_ROOT_PASSWORD                                          -> MySQL默认密码
```




