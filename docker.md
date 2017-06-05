安装docker：
官方教程：https://store.docker.com/editions/community/docker-ce-server-ubuntu

	1. Set up the repository

	sudo apt-get -y install \
	  apt-transport-https \
	  ca-certificates \
	  curl
	
	curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
	
	sudo add-apt-repository \
	       "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
	       $(lsb_release -cs) \
	       stable"
	
	sudo apt-get update
	2. Get Docker CE
	
	Install the latest version of Docker CE on Ubuntu:
	
	sudo apt-get -y install docker-ce
	3. Test your Docker CE installation
	
	Test your installation:
	
	sudo docker run hello-world

在vps上安装报错， 执行：apt-get -f install libltdl7 后正常
在Windows上，无法启动，经排查，是因为360在一次杀毒中把docker的启动项当作病毒处理了，恢复启动项后正常。

2013年docker开源
2014.06 docker 1.0
2015年3月份阿里就用进了生产环境


docker一个应用容器化平台。
标准化

* 传输方式标准化，
* 存储方式标准化，
* api接口标准化，

隔离。使用linux的lxc技术虚拟化。



解决的问题：

* 运行环境不一致导致的运行结果不一样：开发时正常，测试却出问题
* 某一个程序内存泄漏，导致系统整体卡
* 部署简单。从一台快速部署至多台。

docker的运行过程：

1. 构建应用
2. 从仓库把代码传输到本地
3. 用命令将镜像运行起来，虚拟化。运行容器。，

镜像：docker将容项目文件变为镜像：将多个环境打包为一个分层的镜像。

* 可写层
* 镜像层：不可修改，若要修改里面的内容，会将其拷贝到可写层


docker仓库：
* hub.docker.com
* c.163.com
* 自己搭建

查看docker是否安装
使用docker version命令

 	docker version
		Client:
		 Version:      17.03.1-ce
		 API version:  1.27
		 Go version:   go1.7.5
		 Git commit:   c6d412e
		 Built:        Tue Mar 28 00:40:02 2017
		 OS/Arch:      windows/amd64
		
		Server:
		 Version:      17.03.1-ce
		 API version:  1.27 (minimum version 1.24)
		 Go version:   go1.7.5
		 Git commit:   c6d412e
		 Built:        Tue Mar 28 00:40:02 2017
		 OS/Arch:      windows/amd64
		 Experimental: true

linux下安装docker：curl -s https://get.docker.com|sh
启动docker： service docker  start
使用docker version查看安装结果

常用指令：

|指令作用 | 对应指令 |
|---|----|
|查看本机所有镜像 | docker images |
|下载镜像 | docker pull 镜像名|
|运行容器 | docker run 镜像名|
|后台运行容器| docker run -d 镜像名|
|指定端口映射运行容器| docker run -p 1111:11(本机IP:docker内部IP) 镜像名|
|查看正在运行的容器 | docker ps|
|进入容器 | docker exec -it 容器名称 bash|
|停止容器 | docker stop 容器名称|
|创建自己的镜像 | docker build |


例如：


		PS C:\Users\hao19>  docker images
		REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
		PS C:\Users\hao19> docker pull hello-world
		Using default tag: latest
		latest: Pulling from library/hello-world
		78445dd45222: Pull complete
		Digest: sha256:c5515758d4c5e1e838e9cd307f6c6a0d620b5e07e6f927b07d05f6d12a1ac8d7
		Status: Downloaded newer image for hello-world:latest
		PS C:\Users\hao19>  docker images
		REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
		hello-world         latest              48b5124b2768        3 months ago        1.84 kB
		PS C:\Users\hao19> docker run hello-world
		
		Hello from Docker!
		This message shows that your installation appears to be working correctly.
		
		To generate this message, Docker took the following steps:
		 1. The Docker client contacted the Docker daemon.
		 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
		 3. The Docker daemon created a new container from that image which runs the
		    executable that produces the output you are currently reading.
		 4. The Docker daemon streamed that output to the Docker client, which sent it
		    to your terminal.
		
		To try something more ambitious, you can run an Ubuntu container with:
		 $ docker run -it ubuntu bash
		
		Share images, automate workflows, and more with a free Docker ID:
		 https://cloud.docker.com/
		
		For more examples and ideas, visit:
		 https://docs.docker.com/engine/userguide/


docker使用隔离机制保证互不干扰。容器和主机之间会有网络隔离。网络隔离主要有host模式，bridge模式，non模式。
使用端口映射保证从主机能访问到容器网络。

打包步骤：
1. 创建 Dockerfile
2. docker build
		Dockerfile 的内容,以tomcat为例：
			from  hub.c.163.com/library/tomcat
			MAINTAINER hhh xxx@qq.com
			COPY jpress.war /user/local/tomcat/webapps

