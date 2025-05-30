FROM alpine:3.19

# install dependencies; 安装依赖
RUN apk update && apk add --no-cache \
    build-base \
    python3 \
    python3-dev \
    py3-pip \
    py3-setuptools \
    py3-wheel \
    git \
    wget \
    gmp-dev \
    bison \
    flex \
    openssl-dev \
    bash
    

# set pbc, charm-crypto download directory; 设置下载目录
WORKDIR /home/download

# install pbc from source codes; 编译并安装 PBC 库
RUN wget https://crypto.stanford.edu/pbc/files/pbc-0.5.14.tar.gz && \
    tar -xzvf pbc-0.5.14.tar.gz && cd pbc-0.5.14 && \
    ./configure && make && make install

# intall charm-crypto from source codes; 安装 charm-crypto
# Create and activate a virtual environment
RUN python3 -m venv /venv
ENV PATH="/venv/bin:$PATH"
RUN git clone https://github.com/JHUISI/charm.git && \
    cd charm && \
    ./configure.sh && make install && \
    pip3 install .

# clear downloads; 删除源文件
RUN rm -rf /home/download/*

# test if charm-crypto is installed successfully; 测试 charm 安装
RUN python3 -c "from charm.toolbox.pairinggroup import PairingGroup; print('Charm installed successfully with pairing group:', PairingGroup('SS512'))"

# set work directory; 设置工作目录
WORKDIR /home

CMD ["/bin/sh"]
