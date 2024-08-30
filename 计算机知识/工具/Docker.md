## 1. Docker 简介

- **Docker** 是一个开源的应用容器引擎，让开发者可以打包他们的应用以及依赖包到一个可移植的容器中，然后发布到任何流行的 Linux 机器上，也可以实现虚拟化。
- 容器是完全使用沙箱机制，相互之间不会有任何接口（类似 iPhone 的 app）。
- 容器性能开销极低。

## 2. Docker 的三个基本概念

- **镜像（Image）**：Docker 镜像是一个特殊的文件系统，除了提供容器运行时所需的程序、库、资源、配置等文件外，还包含了一些为运行时准备的一些配置参数（如匿名卷、环境变量、用户等）。镜像不包含任何动态数据，其内容在构建之后也不会被改变。
- **容器（Container）**：容器是镜像运行时的实体。容器可以被创建、启动、停止、删除、暂停等。容器的实质是进程，但与直接在宿主执行的进程不同，容器进程运行于属于自己的独立的命名空间。因此容器可以拥有自己的root文件系统、自己的网络配置、自己的进程空间，甚至自己的用户ID空间。
- **仓库（Repository）**：仓库是集中存放镜像文件的场所。Docker 公司提供官方的 Docker Hub 作为默认的镜像仓库，此外，还可以搭建私有的 Docker 仓库。

## 3. 安装 Docker

- Docker 分为 CE（Community Edition，社区版）和 EE（Enterprise Edition，企业版）。
- `docker version` 或 `docker info` 查看是否安装成功
## 4. Docker 镜像操作

- **搜索镜像**：使用 `docker search` 命令。
- **获取镜像**：使用 `docker pull <path_to_image>` 命令从 Docker 仓库下载镜像。
- **列出镜像**：使用 `docker images` 或 `docker image ls` 命令。
- **删除镜像**：使用 `docker rm <image_name>` 命令。
- **构建镜像**：使用 `docker image build -t <iamge_name>:<tag> <dir>`其中，`<dir>`是`Dockerfile`所在目录

## 5. Docker 容器操作

- **运行容器**：使用 `docker container run <image_name>` 命令，可以基于镜像创建一个新的容器并启动它。
- **列出容器**：使用 `docker ps` 命令查看正在运行的容器，`docker ps -a` 查看所有容器（包括未运行的）。
- **停止容器**：使用 `docker stop` 命令。
- **启动已停止的容器**：使用 `docker start` 命令。
- **删除容器**：使用 `docker rm` 命令。

## 6. Docker 容器数据卷

- 容器数据卷（Data Volumes）是 Docker 另一项重要功能，它允许你将一个宿主机上的目录或文件挂载到容器里。
- 数据卷可以在容器之间共享和重用，对数据卷的修改会立马生效，并且更新数据不会影响镜像，实现了数据的持久化。

## 7. DockerFile & .DockerIgnor

- `Dockerfile` 是一个文本文件，包含了一系列的指令，用于指导 Docker 如何构建镜像。
- `.DockerIngnor` 指出了哪些文件不会被包含在镜像中

## 8. Docker 私有仓库
- 搭建 Docker 私有仓库可以存放和分发团队内部的镜像，避免从公网下载。
- 可以使用 Docker Registry 搭建私有仓库。
