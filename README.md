# OpenAI Nginx 反向代理

这个项目是一个使用 Nginx 和 Docker 实现的反向代理，它将本地的请求代理到 OpenAI API。

## 前提条件

你需要在你的服务器上安装以下软件：

- Docker
- Docker Compose

## 安装步骤

### 1. 安装 Docker

在 Ubuntu 上，你可以使用以下命令安装 Docker：

\`\`\`bash
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io
\`\`\`

对于其他 Linux 发行版或操作系统，你可以查看 [Docker 官方文档](https://docs.docker.com/engine/install/) 来获取详细的安装指南。

### 2. 安装 Docker Compose

在 Ubuntu 上，你可以使用以下命令安装 Docker Compose：

\`\`\`bash
sudo curl -L "https://github.com/docker/compose/releases/download/1.28.5/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
\`\`\`

对于其他 Linux 发行版或操作系统，你可以查看 [Docker Compose 官方文档](https://docs.docker.com/compose/install/) 来获取详细的安装指南。

### 3. 部署反向代理

首先，克隆这个仓库到你的服务器：

\`\`\`bash
git clone git@github.com:sandywk/openai_proxy.git
cd your_repository
\`\`\`

然后，使用 Docker Compose 启动服务：

\`\`\`bash
docker-compose up -d
\`\`\`

现在，你的反向代理应该已经启动并运行在 80 端口 。

接下来你需要将你的域名解析到部署的服务器。

## 使用方法

你可以通过发送 HTTP 请求到 来使用这个反向代理。这个反向代理将会将你的请求代理到 https://api.openai.com ，并且保持所有的路径和查询参数不变。
