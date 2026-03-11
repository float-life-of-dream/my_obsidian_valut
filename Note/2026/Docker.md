[TOC]

# Docker

## Docker入门

### Docker介绍 

常规部署（以centos7安装MySQL8为例）

1. 查看系统环境
2. 下载安装包
3. 解压安装包
4. 卸载系统自带的数据库
5. 安装MySQL
6. 查看完成后的安装包
7. 初始MySQL服务
8. 启动MySQL服务
9. 验证

Docker部署（以centos7安装MySQL8为例）

```dockerfile
docker run -d --name ms -p 3306:3306 -e MYSQL_ROOT_PASSWORD=123 mysql
```

### Docker安装(ubuntu)

#### 卸载老版本docker

ubuntu自带的docker版本太低，需要先卸载旧的再安装新的。

注：docker的旧版本不一定被称为docker，docker.io 或 docker-engine也有可能，所以我们卸载的命令为：

```shell
$ apt-get remove docker docker-engine docker.io containerd runc
```

#### 安装步骤

1. 更新软件包

   ```shell
   sudo apt update
   sudo apt upgrade
   ```

   

2. 安装docker依赖

   ```shell
   apt-get install ca-certificates curl gnupg lsb-release
   ```

3. 添加Docker官方GPG密钥

   ~~~shell
   curl -fsSL http://mirrors.aliyun.com/docker-ce/linux/ubuntu/gpg | sudo apt-key add -
   ~~~

4. 添加docker软件源

   ```shell
   sudo add-apt-repository "deb [arch=amd64] http://mirrors.aliyun.com/docker-ce/linux/ubuntu $(lsb_release -cs) stable"
   ```

5. 安装docker

   ```shell
   apt-get install docker-ce docker-ce-cli containerd.io
   ```

6. 配置用户组（可选）
   默认情况下，只有root用户和docker组的用户才能运行Docker命令。我们可以将当前用户添加到docker组，以避免每次使用Docker时都需要使用sudo。命令如下：

   ```shell
    sudo usermod -aG docker $USER
   ```

#### 运行docker

我们可以通过启动`docker`来验证我们是否成功安装。命令如下：

```bash
systemctl start docker
```

#### 安装工具

```bash
apt-get -y install apt-transport-https ca-certificates curl software-properties-common
```

#### 重启docker

```bash
service docker restart
```

#### 验证是否成功

```bash
sudo docker run hello-world
```

#### 查看版本

我们可以通过下面的命令来查看docker的版本

```bash
sudo docker version
```

#### 查看镜像

上面我们拉取了hello-world的镜像，现在我们可以通过命令来查看镜像，命令如下：

```bash
sudo docker images
```

### 部署MySQL

```dockerfile
docker run -d --name mysql -p 3306:3306 -e TZ=Asiz/Shanghai -e MYSQL_ROOT_PASSWORD=123 mysql
```

#### 镜像与容器

docker安装应用是，docker会自动搜索并下载应用镜像（image）

镜像不仅包括应用本身，还包括应用运行所需要的环境、配置、系统函数库

docker会在运行时创建一个隔离环境，称为容器（container）

```dockerfile
docker ps
```

查看是否启动成功

**镜像仓库**：存储和管理镜像的平台，Docker官方维护一个公共仓库:Docker Hub

![](./images/PixPin_2025-02-07_22-53-58.png)

### 命令入门

- docker run ：创建并运行一个容器，-d是让容器在后台运行
- --name mysql ：给容器起一个名字，必须唯一
- -p 3306:3306 ：设置端口映射
- -e KEY=VALUE：是设置环境变量
- mysql ：指定运行的镜像的名字

#### 镜像命名规范

镜像名称一般分两部分组成：[repository]:[tag]

- 其中repository就是镜像名
- tag就是镜像版本

在没有指定tag时，默认时latest，代表最新版本镜像

## Docker基础

### 常见命令

Docker最常见的命令就是操作镜像、容器的命令，详见官方文档：https://docs.docker.com

![](./images/PixPin_2025-02-08_11-02-43.png)

**命令别名**

```bash
vim /root/.bashrc
source /root/.bashrc
```

### 数据卷

 #### 数据卷挂载

数据卷是一个虚拟目录,是容器内目录与宿主机目录之间映射的桥梁

![volume](./images/volume.png)

| 命令                    | 说明               |
| ----------------------- | ------------------ |
| `docker volume create`  | 创建数据卷         |
| `docker volume ls`      | 查看所有数据卷     |
| `docker volume rm`      | 删除指定指定数据卷 |
| `docker volume inspect` | 查看数据卷详情     |
| `docker volume prune`   | 清除数据卷         |

- 当执行`docker run`命令时 ，使用 -v 数据卷:容器内目录 可以完成数据卷挂载
- 当创建容器时，如果挂载了数据卷且数据卷不存在，会自动创建数据卷

#### 本地目录挂载

- 在执行`docker run` 命令时,使用 -v 本地目录:容器内目录可以完成本地目录的挂载
- 本地目录必须以"/"或"./"开头，如果直接以名称开头，会被识别成数据卷而非本地目录
  -  -v mysql : /var/lib/mysql 会被识别为一个数据卷叫mysql
  - -v ./mysql : /var/lib/mysql 会被识别为当前目录下的mysql目录

### 自定义镜像

镜像就是包含了应用程序、程序运行的系统函数库、运行配置等文件的文件包。

构建镜像的过程其实就是把上述文件打包的过程

![](./images/dockerfile.png)

#### 镜像结构

**入口**

镜像运行入口，一般是程序启动的脚本与参数

**层**

添加安装包、依赖、配置等，每次操作都形成新的一层

**基础镜像**

应用依赖的系统函数库、环境、配置、文件等

#### Dockerfile

Dockerfile就是一个文本文件，其中包含一个个指令，用指令来说明要执行什么操作来构建镜像。

Docker可以根据Docker

| 指令       | 说明                                         | 实例                                                         |
| ---------- | -------------------------------------------- | ------------------------------------------------------------ |
| FROM       | 指定基础镜像                                 | FROM centos:6                                                |
| ENV        | 设置环境变量，可在后面的指令使用             | ENV key value                                                |
| COPY       | 拷贝本地文件到镜像指定目录                   | COPY ./jrell.tar.gz /tmp                                     |
| RUN        | 执行linux的shell命令，一般是安装过程的命令   | RUN tar -zxvf  /tmp/jrell.tare.gz && EXPORTS path=/tmp/jrell:$path |
| EXPOSE     | 指定容器运行时监听的端口，是给镜像使用者看的 | EXPOSE 8080                                                  |
| ENTRYPOINT | 镜像中应用启动命令，容器运行时调用           | ENTRYPOINT java -jar xx.jar                                  |

官方文档:https://docs.docker.com/engine/reference/builder

基于Ubuntu基础镜像，也可以使用JDK为基础镜像

当编写好Dockerfile，可以利用下面的命令来构建镜像:

```bash
docker build -t myImage:1.0 .
```

-t：是给镜像起名，格式依然是repository:tag的格式，不指定tag时，默认为latest

.：是指定Dockerfile所在目录，如果就在当前目录，则指定为"."

### 网络

默认情况下所有容器都是以bridge方式连接到Docker的一个虚拟网桥上

加入自定义网络的容器才可以通过容器名互相访问

| 指令                      | 说明                     |
| ------------------------- | ------------------------ |
| docker network create     | 创建一个网络             |
| docker network ls         | 查看所有网络             |
| docker network rm         | 删除指定网络             |
| docker network prune      | 清除未使用网络           |
| docker network connect    | 是指定容器连接加入某网络 |
| docker network disconnect | 是指定容器连接离开某网络 |
| docker network inspect    | 查看网络详细信息         |

## 项目部署

#### DockerCompose

DockerCompose通过一个单独的docker-compose.yml 模板文件（YAML格式）来定义一组相关联的应用容器，帮助我们实现多个相互关联的Docker容器的快速部署

docker compose命令格式如下

```bash
docker compose [OPTIONS][COMMAND]
```

| 类型     | 参数或指令 | 说明                         |
| -------- | ---------- | ---------------------------- |
| Options  | -f         | 指定compose文件的路径和名称  |
|          | -p         | 指定project名称              |
| Commands | up         | 创建并启动所有service容器    |
|          | down       | 停止并移除所有容器、网络     |
|          | ps         | 列出所有启动的容器           |
|          | logs       | 查看指定容器的日志           |
|          | stop       | 停止容器                     |
|          | start      | 启动容器                     |
|          | restart    | 重启容器                     |
|          | top        | 查看运行的进程               |
|          | exec       | 在指定的运行中容器中执行命令 |



