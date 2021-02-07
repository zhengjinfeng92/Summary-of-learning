## docker

软件+环境

一次构建，处处运行



镜像：模板    环境+应用环境   千层饼 一层套一层 	

容器：实例   简易版linux环境+运行的运用

仓库：集中存放镜像文件的场所



制作镜像发布到仓库；拉取镜像，生成容器



容器虚拟化技术

与虚拟机的区别

docker容器与宿主机共享OS

宿主机共享OS上运行虚拟机OS



### docker的安装

- yum install -y epel-release
- yum install -y docker-io



#### 镜像加速器

阿里云镜像





#### docker命令

docker run +镜像名称

docker pull 

docker build

#### 镜像命令

docker images 

docker search  tomcat

docker pull tomcat =  docker pull tomcat:latest

docker rmi 删除镜像 docker rmi -f + 镜像id 镜像id

docker rmi -f $(docker images -qa)

#### 容器命令

新建并启动容器：docker run [OPTIONS] IMAGE [COMMAND] [ARG...] 

前台：-it

后台:-d

-P : 主机端口  -p：内部端口

列出所有正在运行的容器：**docker ps**

在运行的容器中执行命令：**docker exec** 

退出容器： **exit**

启动：docker start +容器名称

重启：docker restart

停止：docker stop +

强制停止：docker kill +

删除已停止的容器：docker rm +容器id





docker日志：docker logs -t -f -tail  + 容器id

查看容器内运行的进程： docker top+ 容器id

查看容器内部细节： docker inspect + 容器id

#### 镜像

底层原理：UnionFS(联合文件系统)

加载原理：

- bootfs
- rootfs

分层的镜像

共享镜像

#### 镜像命令

docker commit + 容器id ：提交容器副本使之成为一个新的镜像

docker pull