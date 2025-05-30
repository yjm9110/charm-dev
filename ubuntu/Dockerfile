FROM ubuntu:22.04

# set environment value to enable interaction during package installation; 设置环境变量来取消包安装过程的交互行为
ENV DEBIAN_FRONTEND=noninteractive

# install dependencies; 安装系统依赖
RUN apt-get update && apt-get install -y \
    build-essential \
    python3 \
    python3-dev \
    python3-pip \
    python3-setuptools \
    python3-wheel \
    git \
    wget \
    libgmp-dev \
    bison \
    flex \
    libssl-dev \
    && rm -rf /var/lib/apt/lists/*

# set pbc, charm-crypto download directory; 进入下载目录
WORKDIR /home/download 
# install pbc from source codes; 安装pbc
RUN wget https://crypto.stanford.edu/pbc/files/pbc-0.5.14.tar.gz && \
    tar -xzvf pbc-0.5.14.tar.gz && cd pbc-0.5.14 && \
    ./configure && make && make install
# RUN git clone https://github.com/blynn/pbc.git && \
#     cd pbc && \
#     libtoolize --force --copy && \
#     aclocal && \
#     autoheader && \
#     automake --add-missing --copy --gnu && \
#     autoconf && \
#     ./configure && make && \
#     make install && \
#     ldconfig

# intall charm-crypto from source codes; 安装 charm-crypto
# RUN pip3 install charm-crypto // failed due to version contradiction
RUN git clone https://github.com/JHUISI/charm.git && \
    cd charm && \
    ./configure.sh && make install && \
    pip3 install .  

# clear downloads; 删除下载的源文件
RUN rm -rf /home/download/*

# test if charm-crypto is installed successfully; 测试 charm 安装
RUN python3 -c "from charm.toolbox.pairinggroup import PairingGroup; print('Charm installed successfully with pairing group:', PairingGroup('SS512'))"

# set work directory; 设置工作目录
WORKDIR /home

CMD ["/bin/bash"]
