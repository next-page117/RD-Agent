FROM pytorch/pytorch:2.2.1-cuda12.1-cudnn8-runtime

# For GPU support, please choose the proper tag from https://hub.docker.com/r/pytorch/pytorch/tags

# 配置清华镜像源
RUN pip config set global.index-url https://pypi.tuna.tsinghua.edu.cn/simple
RUN pip config set global.trusted-host pypi.tuna.tsinghua.edu.cn

# 更新系统包管理器并安装系统依赖
RUN apt-get clean && apt-get update && apt-get install -y \  
    curl \  
    vim \  
    git \  
    build-essential \
    && rm -rf /var/lib/apt/lists/* 

# 克隆 qlib 仓库
RUN git clone https://github.com/microsoft/qlib.git

WORKDIR /workspace/qlib

# 重置到指定提交
RUN git fetch && git reset 3e72593b8c985f01979bebcf646658002ac43b00 --hard

# 使用清华镜像源安装 Python 依赖
RUN python -m pip install --upgrade cython -i https://pypi.tuna.tsinghua.edu.cn/simple
RUN python -m pip install -e . -i https://pypi.tuna.tsinghua.edu.cn/simple

RUN pip install catboost -i https://pypi.tuna.tsinghua.edu.cn/simple
RUN pip install xgboost -i https://pypi.tuna.tsinghua.edu.cn/simple
RUN pip install scipy==1.11.4 -i https://pypi.tuna.tsinghua.edu.cn/simple
RUN pip install tables -i https://pypi.tuna.tsinghua.edu.cn/simple
