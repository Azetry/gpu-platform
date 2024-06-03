# 使用 PyTorch 的基礎映像檔
FROM pytorch/pytorch:latest

# 安裝必要的軟體包
RUN apt-get update && apt-get install -y \
    openssh-server \
    sudo \
    && rm -rf /var/lib/apt/lists/*

# 安裝 JupyterLab
RUN pip install jupyterlab

# 新增使用者並設定密碼
ARG USER_NAME=device
ARG USER_PASSWORD=qwer1234
RUN useradd -m $USER_NAME && echo "$USER_NAME:$USER_PASSWORD" | chpasswd && adduser $USER_NAME sudo

# 將使用者設定為無密碼 sudo
RUN echo "$USER_NAME ALL=(ALL) NOPASSWD: ALL" > /etc/sudoers.d/$USER_NAME

# 設定 SSH
RUN mkdir /var/run/sshd
EXPOSE 22

# 設定 JupyterLab
WORKDIR /home/$USER_NAME
USER $USER_NAME
EXPOSE 8888

# 啟動指令
CMD sudo service ssh start & jupyter lab --ip=0.0.0.0 --port=8888 --no-browser --allow-root