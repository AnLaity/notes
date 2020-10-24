### Docker

#### Centos7 安装 Docker 并配置

- 在 CentOS 7安装docker要求系统为64位、系统内核版本为 3.10 以上，可以使用以下命令查看

```shell script
uname -r
```

- yum 安装 Docker

    - 查看是否安装Docker
     ```shell script
     yum list installed | grep docker
     ```
    - 安装 docker
     ```shell script
     yum -y install docker
     ```
    - Docker运行相关命令
    ```shell script
     systemctl start docker         -> 启动
     systemctl restart docker       -> 重启
     systemctl stop docker          -> 停止
     systemctl start docker         -> 设置开机自启
    ```

- Docker 常用命令

```docker
docker version                          -> 查看 Docker 版本信息
docker inspect                          -> 用于查看镜像和容器的详细信息，默认会列出全部信息，可以通过--format参数来指定输出的模板格式，以便输出特定信息
docker ps                               -> 默认显示当前正在运行中的container
docker ps -a                            -> 查看包括已经停止的所有容器
docker ps -l                            -> 显示最新启动的一个容器（包括已停止的）
docker images                           -> 列出所有镜像
docker search                           -> 搜索镜像
docker pull                             -> 下载镜像
docker rm                               -> 删除容器
docker rmi                              -> 删除镜像
docker logs                             -> 查看日志
docker exec -it                         -> 开启一个交互的终端
```

- 配置 Docker 国内阿里云加速器
    
    - 编辑 daemon.json 文件
    ```shell script
    vim /etc/docker/daemon.json
    ```
    - 文件内容
    ```shell script
     "registry-mirrors": ["https://ufymxqo5.mirror.aliyuncs.com"]
    ```
    - 重启 Docker
    ```shell script
    systemctl restart docker
    ```


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

#### Docker 命令介绍
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




