FROM debian:stretch-slim

# Install necessary dependencies
RUN apt-get update && \
    apt-get install -y \
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

# Download ngx_http_proxy_connect_module source code
RUN wget https://github.com/chobits/ngx_http_proxy_connect_module/archive/refs/tags/v0.0.1.tar.gz && \
    tar -xvf v0.0.1.tar.gz

# Download and extract Nginx source code
RUN curl -O http://nginx.org/download/nginx-1.19.1.tar.gz && \
    tar -xvf nginx-1.19.1.tar.gz

WORKDIR /usr/local/src/nginx-1.19.1

# Compile Nginx from source including ngx_http_proxy_connect_module
RUN ./configure --add-module=../ngx_http_proxy_connect_module-0.0.1 && \
    make && \
    make install

# Clean up unnecessary software and files to reduce image size
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

# Copy Nginx configuration file into image
COPY download_proxy.conf /usr/local/nginx/conf/nginx.conf

# Set Nginx as the default command for the Docker container
CMD ["/usr/local/nginx/sbin/nginx", "-g", "daemon off;"]