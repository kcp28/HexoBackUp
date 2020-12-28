---
title: Docker学习笔记
date: 2020-12-22 16:08:00
tags:
- Docker
categories: 学习笔记系列
---

## Docker简介

Docker是基于Go语言开发的，开源的应用容器引擎，让开发者可以打包他们的应用以及依赖包到一个可移植的镜像中，然后发布到任何流行的 Linux或Windows机器上，也可以实现虚拟化。容器是完全使用沙箱机制，相互之间不会有任何接口。（摘自[Docker百度百科](https://baike.baidu.com/item/Docker/13344470?fr=aladdin)）<!--more-->

- Docker官网：https://www.docker.com/
- Docker官方文档：https://docs.docker.com/  （官方文档很详细的！）
- 仓库地址：https://hub.docker.com/（docker hub 和GitHub作用相似，可以从中上传/下载配置好的docker镜像）

### Docker & 虚拟机

虚拟机：是一种虚拟化技术，可隔离不同环境（需要开多个虚拟机），但比较笨重，空间大（几个G），开启速度慢（几分钟）。

Docker：容器技术，也是一种虚拟化技术，基于镜像，可隔离不同环境（运行镜像即可），小巧，空间小（几M，KB），开启速度快(秒级启动)。

<!--Docker的作用虚拟机的方式 多个APP公用一个开发环境{% asset_img 1.png %}缺点：-->

## Docker的基本组成

Client 客户端 ：运用命令，访问Docker容器

Docker_host: 相当于Docker的服务器，用于真正地运行Docker。

### 镜像（image）

docker镜像就好比是一个模板，可以通过这个模板创建容器服务。

tomcat镜像==>客户端发布run命令==>tomcat1容器（提供服务器）

通过一个镜像可以创建多个容器，最终的服务或项目是运行在容器中的。

如果和java做类比，那么镜像相当于java中的类，是一个模板。而容器相当于对象。一个镜像可以创建多个容器，具体的服务是运行在容器中的

### 容器（container）

容器通过镜像来创建。Docker利用容器技术，独立运行一个或者一组应用。

可以把容器理解为一个简易的linux系统，它具有启动、停止、删除等基本命令，控制服务的执行。

### 仓库（Repository）

仓库是存放镜像的地方。

官方仓库：Docker Hub

仓库分为公有仓库和私有仓库，仓库默认是国外的官方仓库。

国外的仓库访问时速度可能较慢，可以配置镜像加速

国内的像阿里云等都有容器服务器。

## 安装Docker

### Linux(centos7) 

#### 环境准备

最新的docker需要在centos7以上

```shell
#查看os内核版本
uname -r
#查看系统配置
cat /etc/os-release
```

#### 安装Docker

查看官方文档

1.卸载旧的docker

```
yum remove docker \
                  docker-client \
                  docker-client-latest \
                  docker-common \
                  docker-latest \
                  docker-latest-logrotate \
                  docker-logrotate \
                  docker-engine
```

有几种不同的安装方法，这里选择使用仓库安装（install using the repository）

2.下载需要的安装包

```shell
yum install -y yum-utils
```

3.设置镜像的仓库

```shell
#默认是国外的
yum-config-manager \
    --add-repo \
    https://download.docker.com/linux/centos/docker-ce.repo
#推荐使用国内的阿里云镜像，这个下载镜像时比较快
yum-config-manager --add-repo http://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo
```

4.更新yum软件包索引

yum makecache fast

5.安装docker相关的（核心、客户端和容器）

```shell
#安装最新版docker  核心   客户端         容器
yum install docker-ce docker-ce-cli containerd.io
#docker-ce 社区版docker(推荐使用)   docker-ee 企业版docker

#安装指定版本的docker
#查看可安装的docker版本
yum list docker-ce --showduplicates | sort -r

docker-ce.x86_64  3:18.09.1-3.el7                     docker-ce-stable
docker-ce.x86_64  3:18.09.0-3.el7                     docker-ce-stable
docker-ce.x86_64  18.06.1.ce-3.el7                    docker-ce-stable
docker-ce.x86_64  18.06.0.ce-3.el7                    docker-ce-stable
#安装指定版本
yum install docker-ce-<版本号> docker-ce-cli-<版本号> containerd.io
```

至此dockers已经安装成功，下面将启动docker来检测是否安装成功

#### 启动docker

```shell
#启动docker
systemctl start docker
#查看docker版本，确认docker是否启动成功
docker version

```

#### 启动hello world

查看是否安装成功

```shell
docker run hello-world
```

#### 查看已经有的镜像

```shell
docker images
```

#### 卸载docker

```shell
#移除docker相关的依赖
yum remove docker-ce docker-ce-cli containerd.io
#删除docker目录，删除资源
rm -rf /var/lib/docker
#   /var/lib/docker  docker的默认工作路径
```

##### docker run 的运行流程

{% asset_img DockerRun运行流程.png %}

## Docker 底层原理

1. Docker是怎样工作的

   Docker是一个Client-Server结构的系统，Docker的守护进程运行在主机上，通过Socket从客户端访问。

   DockerServer接收到Docker-Client的指令，便执行该指令。

2. Docker为什么比虚拟机快

   Docker有比虚拟机更少的抽象层。

   Docker 利用的是宿主机的内核，vm需要的是GuestOS

   所以，新建一个容器的时候，docker不需想虚拟机一样重新加载一个os内核，避免引导。虚拟机是加载GuestOS 分钟级别的，而docker是利用宿主机的操作系统，省略了这个加载os内核的过程，是秒级的。

## Docker常用命令

### 帮助命令

```shell
docker version  #显示docker的基本信息
docker info     #显示docker的系统信息，包括镜像和容器的数量
docker 命令 --help #帮助命令
```

帮助文档的地址：https://docs.docker.com/reference/

### 镜像命令

docker images    显示所有镜像

```shell
[root@localhost ginsang]# docker images
REPOSITORY    TAG       IMAGE ID       CREATED         SIZE
hello-world   latest    bf756fb1ae65   11 months ago   13.3kB
#解释
EPOSITORY 镜像的仓库源
TAG  镜像的标签
IMAGE ID   镜像的id
CREATED  镜像的创建时间
SIZE   镜像的大小

#可选参数（常用）
-a ,--all  显示所有镜像
-q ,--quiet  只显示镜像id
```

docker search 搜索镜像

```shell
docker search 镜像名
docker search mysql  #搜索mysql镜像
#可选参数
--filter=STARS=3000  #搜索stars数大于3000的
```

docker pull 下载镜像

```shell
docker pull 镜像名[:tag]  #不写tag默认是最新版的
#例子
docker pull mysql
docker pull mysql:5.7  #下载指定版本的镜像
```

docker rmi 删除镜像

```shell
docker rmi -f 镜像名/镜像id  #表示删除指定的镜像
docker rmi -f 镜像名/镜像id 镜像名/镜像id 镜像名/镜像id#同时删除多个镜像
#删除所有镜像
docker rmi -f $(docker images -q)
```

## 容器命令

有了镜像才可以创建容器,下载linux镜像以供测试

docker pull centos

新建容器并启动

```shell
docker run [可选参数] image

#参数说明
--name="Name" 容器名称
-d	后台方式运行
-it	使用交互方式运行，进入容器查看内容
-P	指定容器的端口	-P 8080:8080
	-P ip:主机端口:容器端口
	-P 主机端口:容器端口（常用）
	-P 容器端口
-p	随机指定端口
-rm  用完即删（测试时用）
#若没有下载镜像，则docker run会自动下载，然后再建立启动

#例子
#启动并进入容器
docker run -it centos /bin/bash

#从容器中退出,返回主机
exit
```

docker ps 列出所有运行的容器

```shell
docker ps
#可选参数
 	无参数，表示列出正在运行的容器
 -a	列出正在运行和运行过的容器
 -n=?	显示最近创建的容器。？表示个数 -n=3 显示最近创建的3个容器
 -q	只显示正在运行的容器的id
```

退出容器

```shell
exit #停止并退出容器
ctrl+p+q #容器不停止但退出
```

删除容器

```shell
docker rm 容器id #删除指定的容器，不能删除正在运行的容器
docker rm -f $(docker ps -aq) #删除所有的容器 -f表示强制删除
docker ps -a -q|xargs docker rm #删除所有的容器
```

启动和停止容器的操作

```shell
#docker run相当于创建容器，而docker start是启动创建好的容器
docker start 容器id	#启动容器
docker restart 容器id	#重启容器
docker stop 容器id	#停止当前正在运行的容器
docker kill 容器id	#强制停止当前容器
```

### 常用其他命令

后台启动容器

```shell
#命令 docker run -d 镜像名
docker run -d centos
#当使用docker ps，发现centos停止了
#这是一个常见的坑，docker容器使用后台运行，就必须要有一个前台进程，docker发现前台没有应用就会自动停止
#如nginx 容器启动后，发现自己没有提供服务，就会立即停止
```

查看日志

```shell
docker logs -f -t --tail number 容器id#查看指定容器的日志
#可选参数
-f 持续显示日志
-t 显示时间戳，-t 与-f常写在一起：-tf
--tail number  显示日志的条数
```

查看容器中内部的进程信息

```shell
docker top 容器id
```

查看容器元数据(即容器的信息)

```shell
docker inspect 容器id
```

进入当前正在运行的容器

```shell
#进入容器后开启一个新的终端，可以在里面操作（常用）
docker exec -it 容器id /bin/bash #-it 以交互方式运行
#进入容器正在执行的终端，不会启动新的进程
docker attach 容器id
```

从容器内拷贝文件到主机

```shell
docker cp 容器id:容器内路径 目的主机路径
```

### 常用命令小节

```shell
attach	Attach to a running container				#当前she17 下attach 连接指定运行镜像
build	Build an image from a Dockerfile			#通过Dockerfile定制镜像
commit 	create a new image from a container changes	#提交当前容器为新的镜像
cp 		copy files/folders from the containers filesystem to the host path#从容器中拷贝指定文件或者目录到宿主机中
create	Create a new container						#创建一个新的容器，同run，但不启动容器
diff	Inspect changes on a container's filesystem	#查看docker容器变化
events	Get real time events from the server		#从docker服务获取容器实时事件
exec 	Run a command in an existing container		#在已存在的容器上运行命令
export 	Stream the contents of a container as a tar archive#导出容器的内容流作为一个 tar归档文件[对应import ]
history show the history of an image				#展示一个镜像形成历史
images	List images									#列出系统当前镜像
import 	Create a new filesystem image from the contents of a tarball # 从tar包中的内容创建一个新的文件系统映像[对应export]
info	Display system-wide information				#显示系统相关信息
inspect Return low-level information on a container	#查看容器详细信息
kill	Kill a running container					#kill指定docker容器
load	Load an image from a tar archive			#从一个tar包中加载一个镜像[对应save]
login 	Register or Login to the docker registry server #注册或者登陆一个docker 源服务器
logout	Log out from a Docker registry server		#从当前Docker registry退出
logs	Fetch the logs of a container				#输出当前容器日志信息
port 	Lookup the public-facing port which is NAT-ed to PRIVATE_PORT#查看映射端口对应的容器内部源端口
pause	Pause all processes within a container		#暂停容器
ps		List containers								#列出容器列表
pu11	Pull an image or a repository from the docker registry server # 从docker镜像源服务器拉取指定镜像或者库镜像
push	Push an image or a repository to the docker registry server# 推送指定镜像或者库镜像至docker源服务器
restart	Restart a running container					#重启运行的容器
rm		Remove one or more containers				#移除一个或者多个容器
rmi		Remove one or more images	#移除一个或多个镜像[无容器使用该镜像才可删除，否则需删除相关容器才可继续或-f强制删除]
run		Run a command in a new container			#创建一个新的容器并运行一个命令
save	save an image to a tar archive				#保存一个镜像为一个 tar包[对应1oad]
search	search for an image on the Docker Hub		#在docker hub中搜索镜像
start	start a stopped containers					#启动容器
stop	stop a running containers					#停止容器
tag		Tag an image into a repository				#给源中镜像打标签
top		Lookup the running processes of a container #查看容器中运行的进程信息
unpause	Unpause a paused container					#取消暂停容器
version show the docker version information			#查看docker版本号
wait	Block until a container stops，then print its exit code #截取容器停止时的退出状态值
```

## Docker镜像讲解

### 镜像是什么

镜像是一种轻量级、可执行的独立软件包，用来打包软件运行环境和基于运行环境开发的软件，它包含**运行某个软件所需的所有内容，包括代码、运行时、库、环境变量和配置文件**。

所有的应用，直接打包docker镜像，就可以直接跑起来!

### 如何得到镜像

- 从远程仓库下载
- 朋友拷贝给你
- 自己制作一个镜像DockerFile

### Docker镜像加载原理

#### UnionFS(联合文件系统)

（下载镜像时看到的一层层的就是这个）

UnionFS (联合文件系统): Union文件系统( UnionFS )是一种分层、轻量级并且高性能的文件系统，它**支持对文件系统的修改作为一次提交来一层层的叠加**，同时可以将不同目录挂载到同一个虚拟文件系统下(unite several directories into a single virtualfile system)。Union文件系统是Docker镜像的基础。镜像可以通过分层来进行继承，基于基础镜像（没有父镜像），可以制作各种具体的应用镜像。
特性:一次同时加载多个文件系统，但从外面看起来，只能看到一个文件系统，联合加载会把各层文件系统叠加起来，这样最终的文件系统会包含所有底层的文件和目录。

#### Docker镜像加载原理

docker的镜像实际上由一层一层的文件系统组成，这种层级的文件系统UnionFS.

bootfs(boot file system)主要包含bootloader和kernel, bootloader主要是引导加载kernel(像电脑开机时就在引导加载内核，当os加载完，boot就没用了), Linux刚启动时会加载bootfs文件系统，在Docker镜像的最底层是bootfs。这一层与我们典型的Linux/Unix系统是一样的，包含boot加载器和内核。当boot加载完成之后整个内核就都在内存中了，此时内存的使用权已由bootfs转交给内核，此时系统也会卸载bootfs。

rootfs (root file system)，在bootfs之上。包含的就是典型Linux系统中的/dev,/proc,/bin, /etc等标准目录和文件（就是文件系统）。rootfs就是各种不同的操作系统发行版，比如Ubuntu , Centos等等。

平时我们安装进虚拟机的CentOS都是好几个G，为什么Docker这里才200M ?

```shell
[ root@kuangshen home]# docker images centos
REPOSITORY 	TAG 	IMAGE ID 		CREATED 		SIZE
centos 		latest	470671670cac	3months ago		237MB
```

​	对于一个精简的O5 ， rootfs可以很小，只需要包含最基本的命令，工具和程序库就可以了，因为底层直接用Host的kernel ,自己只需要提供rootfs就可以了。由此可见对于不同的linux发行版, bootfs基本是一致的, rootfs会有差别,因此不同的发行版可以公用bootfs。

Docker镜像都是一层一层下载的，当发现有公用的镜像时，就不再额外下载，直接共用一个。

#### 特点

Docker镜像都是只读的，当容器启动时，一个新的可写层被加载到镜像的顶部！这一层就是我们常说的容器层，容器之下的都叫做镜像层。

### 提交镜像

```shell
命令：docker commit 提交容器成为一个新的副本（镜像）
docker commit -m="提交的描述信息" -a="作者" 容器id 目标镜像名:[TAG]#TAG是版本号
```

如果你想要保存当前容器的状态，就可以通过commit来提交，获得一个镜像，就好比虚拟机的快照。

## Docker 数据卷

### 什么是数据卷

#### dockers的理念

将应用和环境打包成一个镜像。

#### 卷技术

数据是不能在容器中，若数据在容器中，当容器删除时，数据就会丢失！

因此就有了一个需求：让数据可以持久化

容器之间可以有一个数据共享的技术！Docker容器中产生的数据，同步到本地。

这就是卷技术！目录的挂载，将我们容器内的目录，挂载到linux上。

总之，卷技术就是实现**容器的持久化和同步操作，多个容器间也可以数据共享**

只要容器存在，即使容器停止运行了，也可以同步数据。

### 使用数据卷

法一：直接使用命令来挂载 -v

```shell
docker run -it -v 主机目录:容器内目录 #将主机目录和容器内目录作成一个映射,相当于双向绑定；
```

好处：以后修改数据时，在本地修改即可，容器内部数据会自动同步。

即使容器被删除了，我们挂载到本地的数据卷依旧没有丢失，这就实现了容器数据持久化的功能！

### 具名挂载和匿名挂载

```shell
#查看所有Volume（卷）情况
docker volume ls
#查看指定卷的信息
docker volume inspect 卷名
```

#### 匿名挂载

docker run -v 容器内目录

匿名挂载就是仅指定了容器内的路径，没有指定本地主机的路径

所有的docker容器中的卷，在没有指定目录的情况下都是在 /var/lib/docker/volumes/xxxx/_data

#### 具名挂载（常用）

-v 卷名:容器内路径

通过具名挂载可以方便的找到我们的一个卷，大多数情况下使用具名挂载

#### 如何确定具名挂载还是匿名挂载，还是指定路径挂载

```shell
-v 容器内路径			#匿名挂载
-v 卷名:容器内路径		  #具名挂载
-v 宿主机路径:容器内路径	#指定路径挂载
```

```shell
#拓展
#当用-v 卷名:容器内路径:ro/rw 时，表示改变容器内文件的读写权限
#ro readonly  只读，当设置只读时，则说明这个路径只能通过宿主机来操作，容器内部无法操作
#re readwrite 可读

#例子：
docker run -d -p --name nginx02 -v juming-nginx:etc/nginx:ro nginx
docker run -d -p --name nginx02 -v juming-nginx:etc/nginx:rw nginx
```

挂载方式二：通过Dockerfile挂载

### 初识Dockerfile

Dockerfile就是用来构建docker镜像的构建文件。它是一个命令脚本。

通过这个脚本可以生成镜像，镜像是一层一层的，所以脚本是由一个个命令组成的，每个命令都是一层。

```shell
#1.创建Dockerfile文件，命名随意，但推荐使用dockerfile.测试文件内容如下：
FROM Centos  #表示该镜像是以centos为基础的

#构建镜像时挂载。指定的是容器内路径，所以都为匿名挂载。若构建时没有挂载，则只能用-v 卷名:容器内路径  来手动挂载
VOLUME['volume1',"volume2"] 

CMD echo "-----end-----"
CMD /bin/bash

#这里的每个命令（命令都是大写的）都是镜像的一层。
```

#### 建造镜像

```shell
docker build -f dockerfile地址 -t 镜像名:TAG .
#-f 表示dockerfile文件的路径，即根据哪个文件构建镜像
#最后一个.表示当前目录
#注意：各种名称前没有/ 加了/表示是个目录
```

### 数据卷容器

运用数据卷容器来实现多个容器之间数据同步的问题

容器A挂载了容器B，则容器B称为父容器，也叫数据卷容器。

```shell
#运行容器，同时把该容器挂载到父容器上
docker run -it --name 容器名 --volumes-from 父容器 镜像名
```

只要通过 --volumes-from 就可以实现数据共享。

即使数据卷容器被删除了，数据依旧存在，只要有一个容器在使用数据，数据就可存在。

容器之间的数据传递，数据卷容器的生命周期一直持续到没有容器使用它为止。

但当用-v把数据持久化到了本地，则本地数据始终不会被删除。

## DockerFile

### DockerFile简介

dockerFile是用来构建docker镜像的文件，是命令参数脚本

构建镜像步骤：

1、编写一个dockerfile文件

2、docker build构建成为一个镜像

3、docker run运行镜像

4、docker push 发布镜像（Docker Hub、阿里云镜像库）

### 镜像构建步骤

基础知识

1.每个保留关键字（指令）都是大写字母

2.执行从上到下

3.# 表示注释

4.每一个命令都创建一个新的镜像层，并提交

dockerfile是面向开发的，我们以后要发布项目，做镜像，就要编写dockerfile文件，Docker镜像逐渐成为企业标准，必须要掌握。

DockerFile:构建文件，定义了一切的步骤，源代码

DockerImages:通过DockerFile构建生成的镜像，追钟发布和运行的产品

Docker容器：容器就是镜像运行起来提供服务

DockerFile指令

```shell
FROM #基础镜像，一切从这里开始构建
MAINTAINER #镜像作者  姓名+邮箱
RUM #镜像构建的时候要运行的命令
ADD #步骤，添加内容
WORKDIR#镜像的工作目录
VOLUME#挂载的目录
EXPOSE#暴露端口配置
CMD#指定这个容器启动的时候要运行的命令，只有最后一个会生效，可被替代
ENTRYPOINT#指定这个容器启动的时候要运行的命令，可以追加命令
ONBUILD#当构建一个继承dockerFile 这个时候就会执行ONBUILD的指令，触发指令
COPY #类似ADD，将我们文件拷贝到镜像中
ENV#构建的时候设置环境变量
```













































