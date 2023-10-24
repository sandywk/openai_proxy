FROM debian:buster-slim

# 更换 APT 源并清理缓存

RUN apt-get update && \
    apt-get install -y patch \
    wget \
    curl \
    gcc \
    make \
    libpcre3 \
    libpcre3-dev \
    zlib1g \
    zlib1g-dev \
    libssl-dev

WORKDIR /usr/local/src

# 下载 ngx_http_proxy_connect_module 源码
RUN wget https://github.com/chobits/ngx_http_proxy_connect_module/archive/refs/tags/v0.0.5.tar.gz && \
    tar -xzvf v0.0.5.tar.gz

# 下载并解压 Nginx 源码
RUN wget http://nginx.org/download/nginx-1.9.2.tar.gz && \
    tar -xzvf nginx-1.9.2.tar.gz && \
    cd nginx-1.9.2 && \
    patch -p1 < ../ngx_http_proxy_connect_module-0.0.5/patch/proxy_connect.patch

WORKDIR /usr/local/src/nginx-1.9.2

# 从源码编译 Nginx 并包含 ngx_http_proxy_connect_module
RUN ./configure --with-http_ssl_module --add-module=../ngx_http_proxy_connect_module-0.0.5 && \
    make && \
    make install

# 清理不再需要的软件和文件以减小镜像大小
RUN apt-get remove -y \
    wget \
    curl \
    gcc \
    make \
    libpcre3-dev \
    zlib1g-dev \
    libssl-dev && \
    apt-get autoremove -y && \
    rm -rf /var/lib/apt/lists/*

# 将 Nginx 配置文件复制到镜像
COPY download_proxy.conf /usr/local/nginx/conf/nginx.conf

# 设置 Nginx 为 Docker 容器的默认命令
CMD ["/usr/local/nginx/sbin/nginx", "-g", "daemon off;"]