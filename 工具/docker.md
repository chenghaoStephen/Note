##1.Docker是什么##

Docker就是一种虚拟化容器技术。

通过Docker这种虚拟化容器技术，我们可以对物理机的资源进行更加合理有效的利用，可以将一台物理机虚拟化出很多个拥有完整操作系统，并且相互独立的“虚拟计算机”。

**什么是虚拟化？**

虚拟化是一种资源管理技术，是将计算机的各种实体资源，如服务器、网络、内存及存储等，予以抽象、转换后呈现出来，**打破实体结构间的不可切割的障碍，是用户可以比原来的组态更好的方式来应用这些资源。**这些资源的新虚拟部分是不受现有资源的架设方式，地域或物理组态所限制。一般所指的虚拟化资源包括计算能力和资料存储。

在实际的生产环境中，虚拟化技术主要用来解决高性能的物理硬件产能过剩和老旧的硬件产能过低的重组重用，透明化底层物理硬件，从而最大化的利用物理硬件。

**最常用的虚拟化技术：**

**全虚拟化：VMware workstation**

**操作系统虚拟化：Docker**

相对于VMware虚拟化技术，Docker拥有显著的**优势**：

1. 启动速度快；
2. 系统消耗资源低，一台服务器可运行成百上千个Docker容器；
3. 更轻松的迁移和扩展，Docker占用更少的硬盘空间，几乎可以在任意平台上运行。

四个重要概念：

1. 镜像 Image
2. 容器 Container
3. 仓库注册中心 Registry
4. 仓库 Repository

Docker镜像和容器的关系，类似于java中class类与对象之间的关系


## 2.Docker安装 ##

安装之前先卸载：yum -y remove docker

安装：yum install -y docker

启动：systemctl start docker


## 3.Docker镜像 ##

列出镜像：docker images

搜索镜像：docker search tomcat

拉取镜像：

1. 从docker hub拉取，默认，docker pull centos:7，https://hub.docker.com/
2. 从ustc拉取，建议，编辑vi /etc/docker/daemon.json，在配置文件中加入{"registry-mirrors":["https://docker.mirrors.ustc.edu.cn"]}，重启docker服务，systemctl restart docker

删除镜像：docker rmi repository:tag

docker rmi imageID

删除所有镜像 docker rmi $(docker images -q)

导出镜像：docker save -o mynginx.tar mynginx

导入镜像：docker load -i mynginx.tar

## 4.Docker容器 ##
容器命令：docker run

-i 运行容器

-t 容器启动后进入命令行

--name 命名

-v 目录映射（前者是宿主机目录，后者是映射到宿主机上的目录）


-d 创建一个守护式容器在后台运行

-p 端口映射，前者是宿主机端口，后者是容器端口

以交互方式运行容器：
docker run -it --name xxx imageID /bin/bash

以守护进程方式运行容器：
docker run -di --name xxx imageId

注：创建并进入容器后，如果exit退出容器，则容器停止，再次进入，先试用start启动容器，在使用exec或者attach进入容器。

启动容器：docker start 容器名称/ID

进入容器：
docker exec -it 容器名称/ID /bin/bash

docker attach 容器名称/ID

exec/attach的区别：attach进入容器后，使用exit退出，容器停止；exec不会停止。

查看容器：
正在运行的容器：docker ps

历史运行过的容器：docker ps -a

最近运行过的容器：docker ps -l

停止容器：docker stop 容器名称/ID

删除容器：docker rm 容器名称/ID

删除所有容器：docker rm 'docker ps -a -q'

复制文件：docker cp /root/boot.war my-centos:/usr/local/




