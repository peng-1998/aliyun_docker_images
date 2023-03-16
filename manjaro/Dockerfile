from manjarolinux/base:latest

RUN && echo "Server = https://mirrors.tuna.tsinghua.edu.cn/manjaro/stable/\$repo/\$arch" >/etc/pacman.d/mirrorlist &&
    pacman -Syyu --noconfirm &&
    pacman -S --noconfirm cuda python-pip zsh openssh unzip yay sudo curl oh-my-zsh-git oh-my-zsh-plugin-autosuggestions oh-my-zsh-plugin-syntax-highlighting code-server && pacman -Sc --noconfirm &&
    sed -i 's/plugins=(git)/plugins=(git zsh-autosuggestions zsh-syntax-highlighting)/g' ~/.zshrc &&
    ssh-keygen -A &&
    echo "PermitRootLogin yes" >>/etc/ssh/sshd_config &&
    pip config set global.index-url https://pypi.tuna.tsinghua.edu.cn/simple

RUN pip install numpy scipy matplotlib scikit-learn scikit-image opencv-python jupyter tqdm &&
    pip install torch torchvision

# 设置 jupyter notebook password 使用自己的校验码,这里使用的校验码是"scnu"的校验码,注意加\转义
RUN jupyter notebook --generate-config &&
    echo "c.NotebookApp.ip='*'" >>~/.jupyter/jupyter_notebook_config.py &&
    echo "c.NotebookApp.password = 'argon2:\$argon2id\$v=19\$m=10240,t=10,p=8\$xvz0mi9pHX3lpKLqGdRBvA\$Y8xqw2CEvwzORmkM9+bHOFgWHT/TmRewsfd4F7yqmJU'" >>~/.jupyter/jupyter_notebook_config.py && echo "c.NotebookApp.port = 8888" >>~/.jupyter/jupyter_notebook_config.py &&
    echo "c.NotebookApp.allow_remote_access = True" >>~/.jupyter/jupyter_notebook_config.py

# 设置Code-Server code-server的默认端口为8080,以下是默认配置,可以自行使用sed命令修改
# bind-addr: 127.0.0.1:8080
# auth: password
# password: *****
# cert: false
RUN sed -i 's/127.0.0.1/0.0.0.0/g' ~/.config/code-server/config.yaml &&
    sed -i '3c password: scnu' ~/.config/code-server/config.yaml
# 如果不开启jupyter notebook 也要替换成bash指令,否则执行完service ssh start容器就退出了
RUN echo "root:scnu" | chpasswd &&
    echo "/bin/sshd -D &" >/start.sh &&
    echo "code-server &" >>/start.sh &&
    echo "jupyter notebook" >>/start.sh
    

WORKDIR /root/

CMD sh /root/start.sh
