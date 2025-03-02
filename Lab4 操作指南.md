# Lab4 操作指南

1. &zwnj;**在虚拟机中安装 Docker**&zwnj;
   
   ```bash
      sudo apt install docker.io
   ```
<div align="center">
  <img src="image/1.png" width="80%" />
</div>

2. &zwnj;**编写 Dockerfile**&zwnj;
   - 创建一个名为 Dockerfile 的文件，并添加以下内容：
   ```bash
      FROM ubuntu:latest
      RUN apt-get update && apt-get install -y cowsay fortune iputils-ping
   ```

3. &zwnj;**构建Dockerfile**&zwnj;
   - 在包含 Dockerfile 的目录中运行以下命令来构建 Docker 镜像：
   ```bash
      docker build -t cowsay .
   ```
<div align="center">
  <img src="image/6.png" width="80%" />
</div>
<div align="center">
  <img src="image/3.png" width="80%" />
</div>

4. &zwnj;**进入容器并运行 cowsay**&zwnj;
   - 启动一个容器：
   - 在容器内运行 cowsay 命令（假设已进入容器）：
   ```bash
      docker run -it cowsay /bin/bash
      /usr/games/cowsay "Moo"
   ```

<div align="center">
  <img src="image/12.png" width="80%" />
  <img src="image/3.png" width="80%" />
</div>

5. &zwnj;**查看 Docker 进程**&zwnj;
   - 运行以下命令查看正在运行的 Docker 容器：
  
<div align="center">
  <img src="image/13.png" width="80%" />
</div>


6. &zwnj;**创建自定义网络**&zwnj;
   - 创建一个名为 myNetwork 的自定义 Docker 网络：
   ```bash
     docker network create myNetwork
   ```
   
<div align="center">
  <img src="image/14.png" width="80%" />
</div>

7. &zwnj;**创建并连接容器到自定义网络**&zwnj;
   - 创建两个容器
   ```bash
    docker run -it --name mycontainer1 cowsay /bin/bash
    docker run -it --name mycontainer2 cowsay /bin/bash
   ```
   - 将这两个容器连接到 myNetwork 网络：
   ```bash
    docker network connect myNetwork mycontainer1
    docker network connect myNetwork mycontainer2
   ```
<div align="center">
  <img src="image/14.png" width="80%" />
</div>

8. &zwnj;**测试容器间网络连接**&zwnj;
   - 进入第一个容器内，ping通第二个容器网络
   ```bash
    docker exec -it mycontainer1 /bin/bash
    ping 172.18.0.3

   ```
<div align="center">
  <img src="image/15.png" width="80%" />
</div>
