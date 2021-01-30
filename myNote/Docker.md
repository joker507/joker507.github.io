# Docker 入门到使用 -- Linux 

> 为了避免误导别人，如果内容有问题请麻烦指正：2528044459@qq.com



[toc]

### 使用思路

* 获取环境(镜像)
* 运行容器\启动容器
* 运行程序
* 保存\关闭容器



## 概念介绍

* image 镜像 

  也就是一台配置好环境的“虚拟机”模板

  

* 容器

  启动的“虚拟机”，可以运行所需要的程序，当关掉容器的时候，在“虚拟机”上之前运行或者改变的东西会被抹掉，但是可以创建快照保存并打包成镜像。

  

* 仓库（Docker Hub)
  一个庞大的网络仓库所有的官方镜像和公开、私人镜像都保存在仓库。  
  在使用的时候后可以预先把镜像拉去到本地、或者直接启动容器当启动容器所需要的镜像在本地没有的话会自动在仓库中搜索并且拉取下来。

* 其他：多容器管理工具、docker machine托管工具等等。。



***



## docker 应用场景

* Web 应用的自动化打包和发布。
* 自动化测试和持续集成、发布。
* 在服务型环境中部署和调整数据库或其他的后台应用。
* 从头编译或者扩展现有的 OpenShift 或 Cloud Foundry 平台来搭建自己的 PaaS 环境。

***



## Docker 的安装

* Ubuntu：

  1. 通过官方命令自动安装脚本：

> `curl -fsSL https://get.docker.com | bash -s docker --mirror Aliyun`  

2.  通过 国内daocloud 一键安装：（网速快）
> `curl -sSL https://get.daocloud.io/docker | sh`

3. 手动安装：（不太建议麻烦）

   * 这里不详细介绍：[地址在这里可以看看](https://www.runoob.com/docker/ubuntu-docker-install.html)

   

***



## Docker 快速使用: 



### 一、容器 :

1. ### 容器的创建(启动):  (运行程序  	交互式	    后台模式)

命令格式：

```shell
docker run *
```

* 你可以在Docker 的容器里面运行一个应用程序    

~~~shell
```shell
runoob@runoob:~$ docker run ubuntu:15.10 /bin/echo "Hello world"

Hello world
```
~~~


>  参数详解:
>
> - **docker:** Docker 的二进制执行文件。
> - **run:** 与前面的 docker 组合来运行一个容器。
> - **ubuntu:15.10** 指定要运行的镜像，Docker 首先从本地主机上查找镜像是否存在，如果不存在，Docker 就会从镜像仓库 Docker Hub 下载公共镜像。ubuntu 表示仓库源名称（我理解为是镜像）后面的15.10表示TAG（标签，也就是镜像版本）
> - **/bin/echo "Hello world":** 在启动的容器里执行的命令
>
> 以上命令完整的意思可以解释为：Docker 以 ubuntu15.10 镜像创建一个新容器，然后在容器里执行 bin/echo "Hello world"，然后输出结果。

* 运行一个交互式的容器

```shell
runoob@runoob:~$ docker run -i -t ubuntu:15.10 /bin/bash
root@0123ce188bd8:/#
```

> 参数详解
>
> **-t:** 在新容器内指定一个伪终端或终端。
>
> **-i:** 允许你对容器内的标准输入 (STDIN) 进行交互。
>
> - **/bin/bash**：放在镜像名后的是命令，这里我们希望有个交互式 Shell，因此用的是 /bin/bash。
>
> 注意第二行 **root@0123ce188bd8:/#**，此时我们已进入一个 ubuntu15.10 系统的容器



*  启动后台模式容器 

  ```shell
docker run -d ubuntu:15.10 /bin/sh -c "while true; do echo hello world; sleep 1; done"
  ```

>参数
>
>-d 后台模式
>
>ubuntu:15.10 基于镜像启动容器
>
>/bin/sh 启动应用程序
>
>-c "while true; do echo hello world; sleep 1; done" 使用sh 执行的语句
>
>
>
>相当于在终端里面 输入 sh -c while true; do echo hello world; sleep 1; done 这条语句



查看容器状态:

```shell
docker ps 

# 输出结果:
CONTAINER ID        IMAGE                  COMMAND     ...        
5917eac21c36        ubuntu:15.10           "/bin/sh -c 'while t…"    ...
```

> 参数详解：
>
> **CONTAINER ID:** 容器 ID。
>
> **IMAGE:** 使用的镜像。
>
> **COMMAND:** 启动容器时运行的命令。
>
> **CREATED:** 容器的创建时间。
>
> **STATUS:** 容器状态。
>
> 状态有7种：
>
> - created（已创建）
> - restarting（重启中）
> - running（运行中）
> - removing（迁移中）
> - paused（暂停）
> - exited（停止）
> - dead（死亡）
>
> **PORTS:** 容器的端口信息和使用的连接类型（tcp\udp）。
>
> **NAMES:** 自动分配的容器名称。



停止容器

```shell
docker stop id
```

+++



### 二、镜像使用

#### 1. 管理本地和使用Docker 主机镜像（查看、拉取、创建、删除）

* **查看**并列出本机上的镜像：

```shell
docker images
```

```
REPOSITORY   TAG       IMAGE ID      CREATED        SIZE
ubuntu       14.04   90d5884b1ee0    5 days ago     188 MB
php          5.6     f40e9e0f10c8    9 days ago     444.8 MB
```

>参数详解：
>
>- **REPOSITORY：**表示镜像的仓库源
>- **TAG：**镜像的标签
>- **IMAGE ID：**镜像ID
>- **CREATED：**镜像创建时间
>- **SIZE：**镜像大小
>
>TAG : 同一个仓库源可以有多个TAG 表示不同的版本

* 如果你本地没有镜像的话：则你可以使用`docker pull imgname:TAG`来**拉取镜像**

```shell
Crunoob@runoob:~$ docker pull ubuntu:13.10
13.10: Pulling from library/ubuntu
6599cadaf950: Pull complete 
23eda618d451: Pull complete 
f0be3084efe9: Pull complete 
52de432f084b: Pull complete 
a3ed95caeb02: Pull complete 
Digest: sha256:15b79a6654811c8d992ebacdfbd5152fcf3d165e374e264076aa435214a947a3
Status: Downloaded newer image for ubuntu:13.10
```

> 初出现了Status: Downloaded newer image for ubuntu:13.10 表示拉取成功



* 如果你不确定是否有这个镜像的时候你可以用`docker search imgname`在 [Docker Hub]( **https://hub.docker.com/**)上面**搜索镜像**。然后就可以 使用 docker pull  imaname 下来到本地。

> 具体参数：
>
> **NAME:** 镜像仓库源的名称
>
> **DESCRIPTION:** 镜像的描述
>
> **OFFICIAL:** 是否 docker 官方发布
>
> **stars:** 类似 Github 里面的 star，表示点赞、喜欢的意思。
>
> **AUTOMATED:** 自动构建

* **删除镜像**：

  ```shell
  docker rmi imgname
  ```

* **创建镜像**：当我们不满足官方的镜像时，我们可以有两种方法DIY一个镜像。

  *  **从一创建的容器中更新镜像，并且 提交这个镜像**

   * **使用Dockerfile指令创建一个新的镜像**

     

  1. 更新法（创建-修改-更新-退出-提交）：


使用一个镜像**创建**一个容器（启动终端交互式容器）

```shell
runoob@runoob:~$ docker run -t -i ubuntu:15.10 /bin/bash
root@e218edb10161:/# 
```

> （要记住容器的ID，此容器的ID:就为这里显示的本机名字e218edb10161，在提交的时候需要用到）

* 在容器内进行所需的**更改**（比如**安装一个python** `apt install python ` 使用apt安装python的时候先进行一个软件更新和软件列表更新,也就是执行`apt update 和 apt -y upgrade`这两条命令）
* **更新**容器：使用**`apt-get update`**命令进行更新

* **退出**容器:`exit` 完成退出

* **提交**容器：`docker commit *`

```shell
runoob@runoob:~$ docker commit -m="has update" -a="runoob" e218edb10161 runoob/ubuntu:v2

sha256:70bf1840fd7c0d2d8ef0a42a817eb29f854c1af8f7c59fc03ac7bdee9545aff8
```

> 参数详解：
>
> - **m:** 提交的描述信息
> - **-a:** 指定镜像作者
> - **e218edb10161：**容器 ID
> - **runoob/ubuntu:v2:** 指定要创建的目标镜像名
>
> 

1. 使用Dockerfile构建法(在同一目录下建新Dockerfile文件-使用build构建- 设置镜像标签)：
2. 首先我们来了解用来构建镜像的Dockerfile结构吧：



```shell
runoob@runoob:~$ cat Dockerfile 
FROM    centos:6.7
MAINTAINER      Fisher "fisher@sudops.com"

RUN     /bin/echo 'root:123456' |chpasswd
RUN     useradd runoob
RUN     /bin/echo 'runoob:123456' |chpasswd
RUN     /bin/echo -e "LANG=\"en_US.UTF-8\"" >/etc/default/local
EXPOSE  22
EXPOSE  80
CMD     /usr/sbin/sshd -D
```

> 
>
> 每一条指令都会在镜像上面建新一个新的层，指令前缀都要大写
>
> * FROM  表示这个新建镜像的基础镜像
>
> * RUN 表示在镜像内执行的命令
>
>   RUN 太多会导致镜像过于臃肿，我们可以将其改写为一层：
>
>   ```txt
>   RUN  /bin/echo 'root:123456' |chpasswd
>        &&useradd runoob
>        &&/bin/echo 'runoob:123456' |chpasswd
>        &&/bin/echo -e "LANG=\"en_US.UTF-8\""
>   ```
>
> * EXPOSE  设置监听端口
>
> * COPY 复制文件；`COPY <源路径>... <目标路径>`
>
> * ADD 更高级的复制文件`ADD <源路径>... <目标路径>`
>
> * ENV 设置环境变量
>
> * WORKDIR 指定工作目录，在RUN等其他命令前，这些命令会在工作目录下执行
>
> * USER 指定用户 USER deamon
>
> * CMD 指定启动容器时要执行的命令主要有三种格式
>
>   ```shell
>   CMD ["executable","param1","param2"]
>   CMD ["param1","param2"]
>   CMD command param1 param2
>   ```
>
> * ENTRYPOINT 配置一个默认程序，启动就会执行
>
>   ```shell
>   ENTRYPOINT ["executable", "param1", "param2"]
>   ENTRYPOINT command param1 param2
>   ```
>
> * 等等，详细请看[这里](http://www.ityouknow.com/docker/2018/03/15/docker-dockerfile-command-introduction.html)

* 写好Dockerfile后使用docker biuld * 命令创建



```shell
runoob@runoob:~$ docker build -t runoob/centos:6.7 .
Sending build context to Docker daemon 17.92 kB
Step 1 : FROM centos:6.7
 ---&gt; d95b5ca17cc3
Step 2 : MAINTAINER Fisher "fisher@sudops.com"
 ---&gt; Using cache
 ---&gt; 0c92299c6f03
Step 3 : RUN /bin/echo 'root:123456' |chpasswd
 ---&gt; Using cache
 ---&gt; 0397ce2fbd0a
Step 4 : RUN useradd runoob
......
```

> - **-t** ：指定要创建的目标镜像名
> - **.** ：Dockerfile 文件所在目录，可以指定Dockerfile 的绝对路径



* 用镜像启动容器（也就是上面的容器启动命令）



```
docker run *
```



