#### 安装Redis

**docker部署**

``` shell
# 下载镜像
docker pull redis

# 检查当前所有Docker下载的镜像
docker images

## 创建目录
mkdir -p /opt/redis/conf
mkdir -p /opt/redis/data

## 创建文件
touch /opt/redis/conf/redis.conf

# Docker 创建 Redis 容器命令
docker run \
--restart=always \
--log-opt max-size=100m \
--log-opt max-file=2 \
-p 6379:6379 \
--name redis \
-v /opt/redis/conf/redis.conf:/etc/redis/redis.conf  \
-v /opt/redis/data:/data \
-d redis redis-server /etc/redis/redis.conf \
--appendonly yes \
--requirepass 123456 

# 修改 /opt/redis/conf/redis.conf
protected-mode no
bind 0.0.0.0

# 重启redis服务
docker restart redis
```

1. 获取Redis镜像

2. 下载Redis镜像

3. 创建redis配置文件

   1. 启动前需要先创建Redis外部挂载的配置文件 （ /home/redis/conf/redis.conf ）
   2. 之所以要先创建 , 是因为Redis本身容器只存在 /etc/redis 目录 , 本身就不创建 redis.conf 文件
   3. 当服务器和容器都不存在 redis.conf 文件时, 执行启动命令的时候 docker 会将 redis.conf 作为目录创建 , 这并不是我们想要的结果 。

4. 创建Redis容器并启动

| 命令                                                         | 功能                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| docker run                                                   | 这是 Docker 用来创建并运行一个新的容器的命令                 |
| --restart=always                                             | 如果容器退出，这个选项会使得它自动重启                       |
| --log-opt max-size=100m                                      | 这是对容器日志的设置，最大大小为 100MB                       |
| --log-opt max-file=2                                         | 这是对容器日志文件的设置，最多可以有2个日志文件              |
| -p 6379:6379                                                 | 这是端口映射的设置，将宿主机的6379端口映射到容器的6379端口   |
| --name redis                                                 | 这是给新创建的容器命名的选项，名字是 "redis"                 |
| -v /opt/myredis/redis.conf:/etc/redis/redis.conf             | 这是对容器内的文件系统的挂载设置，将宿主机上的 /opt/myredis/redis.conf 文件挂载到容器内的 /etc/redis/redis.conf 位置 |
| -v /opt/myredis/data:/data                                   | 这是另一个文件系统的挂载选项，将宿主机上的 /opt/myredis/data 目录挂载到容器内的 /data目录 |
| -d                                                           | 这是 Docker 的分离模式，新创建的进程将会在后台运行           |
| redis redis-server /etc/redis/redis.conf --appendonly yes --requirepass 123456 | 这是容器内要运行的命令，启动 Redis 服务，使用 /etc/redis/redis.conf 配置文件，设置追加写入(appendonly)为 yes，设置密码为 "123456" |

5. Redis配置文件修改

| 命令              | 功能                                                         |
| ----------------- | ------------------------------------------------------------ |
| protected-mode no | 关闭protected-mode模式，此时外部网络可以直接访问 (docker貌似自动开启了) |
| bind 0.0.0.0      | 设置所有IP都可以访问 (docker貌似自动开启了)                  |

6. RDM 远程连接