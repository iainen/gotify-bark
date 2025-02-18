# gotify-bark

A simple program forward gotify message to bark
(将Gotify消息转发到Bark的程序)

### Supported Platforms:

- amd64 (64bit)
- arm64 (ARMv8)

## Table of Contents
- [Docker Installation](#docker-installation)
  - [Prerequisites](#prerequisites)
  - [Steps](#steps)

- [Docker安装](#docker安装)
  - [前提条件](#前提条件)
  - [步骤](#步骤)


## Docker Installation

### Prerequisites
- Docker must be installed on your system.
- You need to have a running instance of `gotify/server` and `bark-server`. You can set them up by referring to the following links:
  - [gotify/server](https://github.com/gotify/server)
  - [Finb/bark-server](https://github.com/Finb/bark-server)

### Steps
1. Create a directory for the data and environment files. For example, you can create a directory named `/var/gotify-bark` and place the `.env` file inside it. You can refer to [.env.example](.env.example) for the content of the `.env` file.
2. Build the Docker image as described in the [Docker Compilation](#docker-compilation) section.
3. Run the Docker container using the following command:
   ```bash
   docker run -d --restart unless-stopped -e TZ="Europe/Berlin" --env-file /var/gotify-bark/.env --name gotify-bark -p 8080:8080 -v /var/gotify-bark/data:/app/data ghcr.io/bnsui/gotify-bark 
   ```
   - `-d`: Run the container in detached mode (in the background).
   - `--restart unless-stopped`: Restart the container unless it is explicitly stopped.
   - `-e TZ="Europe/Berlin"`: Set the time zone for the container. You can change this value according to your needs.
   - `--env-file /var/gotify-bark/.env`: Load the environment variables from the specified `.env` file.
   - `--name gotify-bark`: Name the container `gotify-bark`.
   - `-p 8080:8080`: Map port 8080 on the host to port 8080 in the container.
   - `-v /var/gotify-bark/data:/app/data`: Mount the host directory `/var/gotify-bark/data` to the container directory `/app/data` to store the database file (if sqlite is used).


## Docker安装

### 前提条件
- 你的系统上必须安装Docker。
- 你需要有一个正在运行的 `gotify/server` 和 `bark-server` 实例。你可以通过参考以下链接来设置它们：
  - [gotify/server](https://github.com/gotify/server)
  - [Finb/bark-server](https://github.com/Finb/bark-server)

### 步骤
1. 创建一个用于存储数据和环境文件的目录。例如，你可以创建一个名为 `/var/gotify-bark` 的目录，并将 `.env` 文件放在其中。你可以参考 [.env.example](.env.example) 来获取 `.env` 文件的内容。
2. 按照 [Docker编译](#docker编译) 部分的说明构建Docker镜像。
3. 使用以下命令运行Docker容器：
   ```bash
   docker run -d --restart unless-stopped -e TZ="Asia/Shanghai" --env-file /var/gotify-bark/.env --name gotify-bark -p 8080:8080 -v /var/gotify-bark/data:/app/data ghcr.io/bnsui/gotify-bark:latest 
   ```
   - `-d`: 以分离模式（在后台）运行容器。
   - `--restart unless-stopped`: 除非明确停止，否则重启容器。
   - `-e TZ="Asia/Shanghai"`: 设置容器的时区。你可以根据需要更改此值。
   - `--env-file /var/gotify-bark/.env`: 从指定的 `.env` 文件加载环境变量。
   - `--name gotify-bark`: 将容器命名为 `gotify-bark`。
   - `-p 8080:8080`: 将主机的端口8080映射到容器的端口8080。
   - `-v /var/gotify-bark/data:/app/data`: 将主机目录 `/var/gotify-bark/data` 挂载到容器目录 `/app/data` 以存储数据库文件（如果使用sqlite）。
  
