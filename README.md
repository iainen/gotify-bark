# gotify-bark

[A simple program forward gotify message to bark](#简单的将Gotify消息转发到Bark的程序)

### Supported Platforms:

- amd64 (64bit)
- arm64 (ARMv8)

## Table of Contents
- [Docker Compilation](#docker-compilation)
- [Docker Installation](#docker-installation)
  - [Prerequisites](#prerequisites)
  - [Steps](#steps)
  - [Example](#example)
- [简单的将Gotify消息转发到Bark的程序](#简单的将Gotify消息转发到Bark的程序)
  - [Docker编译](#docker编译)
  - [Docker安装](#docker安装)
    - [前提条件](#前提条件)
    - [步骤](#步骤)
    - [示例](#示例)

## Docker Compilation

### Dockerfile
The `Dockerfile` is used to build the Docker image for the `gotify-bark` application. Here is the content of the `Dockerfile`:

```Dockerfile
# Use the official Golang image as the base image
FROM golang:1.22 AS builder

# Set the working directory inside the container
WORKDIR /app

# Copy the source code into the container
COPY . .

# Download the dependencies
RUN go mod download

# Build the binary
RUN go build -v -o gotify-bark ./cmd/gotify-bark

# Use a lightweight Alpine image as the final base image
FROM alpine:latest

# Set the working directory inside the container
WORKDIR /app

# Copy the binary from the builder stage
COPY --from=builder /app/gotify-bark .

# Expose the port the application will run on
EXPOSE 8080

# Set the entry point for the container
ENTRYPOINT ["./gotify-bark"]
```

### Compilation Steps
To build the Docker image, follow these steps:

1. Make sure you have Docker installed on your system.
2. Navigate to the root directory of the `gotify-bark` project in your terminal.
3. Run the following command to build the Docker image:
   ```bash
   docker build -t bnsui/gotify-bark .
   ```
   This command will build the Docker image with the tag `bnsui/gotify-bark`.

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
   docker run -d --restart unless-stopped -e TZ="Europe/Berlin" --env-file /var/gotify-bark/.env --name gotify-bark -p 8080:8080 -v /var/gotify-bark/data:/app/data bnsui/gotify-bark
   ```
   - `-d`: Run the container in detached mode (in the background).
   - `--restart unless-stopped`: Restart the container unless it is explicitly stopped.
   - `-e TZ="Europe/Berlin"`: Set the time zone for the container. You can change this value according to your needs.
   - `--env-file /var/gotify-bark/.env`: Load the environment variables from the specified `.env` file.
   - `--name gotify-bark`: Name the container `gotify-bark`.
   - `-p 8080:8080`: Map port 8080 on the host to port 8080 in the container.
   - `-v /var/gotify-bark/data:/app/data`: Mount the host directory `/var/gotify-bark/data` to the container directory `/app/data` to store the database file (if sqlite is used).

### Example
Here is an example of running the Docker container:
```bash
$ docker run -d --restart unless-stopped -e TZ="Asia/Shanghai" --env-file /var/gotify-bark/.env --name gotify-bark -p 8080:8080 -v /var/gotify-bark/data:/app/data bnsui/gotify-bark
```

## 简单的将Gotify消息转发到Bark的程序

### Docker编译

#### Dockerfile
`Dockerfile` 用于构建 `gotify-bark` 应用的Docker镜像。以下是 `Dockerfile` 的内容：

```Dockerfile
# 使用官方的Golang镜像作为基础镜像
FROM golang:1.22 AS builder

# 设置容器内的工作目录
WORKDIR /app

# 将源代码复制到容器中
COPY . .

# 下载依赖项
RUN go mod download

# 构建二进制文件
RUN go build -v -o gotify-bark ./cmd/gotify-bark

# 使用轻量级的Alpine镜像作为最终基础镜像
FROM alpine:latest

# 设置容器内的工作目录
WORKDIR /app

# 从构建阶段复制二进制文件
COPY --from=builder /app/gotify-bark .

# 暴露应用程序运行的端口
EXPOSE 8080

# 设置容器的入口点
ENTRYPOINT ["./gotify-bark"]
```

#### 编译步骤
要构建Docker镜像，请按照以下步骤操作：

1. 确保你的系统上已安装Docker。
2. 在终端中导航到 `gotify-bark` 项目的根目录。
3. 运行以下命令来构建Docker镜像：
   ```bash
   docker build -t bnsui/gotify-bark .
   ```
   此命令将使用标签 `bnsui/gotify-bark` 构建Docker镜像。

### Docker安装

#### 前提条件
- 你的系统上必须安装Docker。
- 你需要有一个正在运行的 `gotify/server` 和 `bark-server` 实例。你可以通过参考以下链接来设置它们：
  - [gotify/server](https://github.com/gotify/server)
  - [Finb/bark-server](https://github.com/Finb/bark-server)

#### 步骤
1. 创建一个用于存储数据和环境文件的目录。例如，你可以创建一个名为 `/var/gotify-bark` 的目录，并将 `.env` 文件放在其中。你可以参考 [.env.example](.env.example) 来获取 `.env` 文件的内容。
2. 按照 [Docker编译](#docker编译) 部分的说明构建Docker镜像。
3. 使用以下命令运行Docker容器：
   ```bash
   docker run -d --restart unless-stopped -e TZ="Europe/Berlin" --env-file /var/gotify-bark/.env --name gotify-bark -p 8080:8080 -v /var/gotify-bark/data:/app/data bnsui/gotify-bark
   ```
   - `-d`: 以分离模式（在后台）运行容器。
   - `--restart unless-stopped`: 除非明确停止，否则重启容器。
   - `-e TZ="Europe/Berlin"`: 设置容器的时区。你可以根据需要更改此值。
   - `--env-file /var/gotify-bark/.env`: 从指定的 `.env` 文件加载环境变量。
   - `--name gotify-bark`: 将容器命名为 `gotify-bark`。
   - `-p 8080:8080`: 将主机的端口8080映射到容器的端口8080。
   - `-v /var/gotify-bark/data:/app/data`: 将主机目录 `/var/gotify-bark/data` 挂载到容器目录 `/app/data` 以存储数据库文件（如果使用sqlite）。
