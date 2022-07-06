from manjarolinux/base:latest
RUN pacman -Syyu --noconfirm \
    && pacman -S --noconfirm cuda python-pip zsh openssh unzip yay\
    && pacman -Sc --noconfirm \
    && ssh-keygen -A

COPY ./src/sshd_config /etc/ssh/

COPY ./src/.oh-my-zsh.zip /root/

RUN unzip -q -d /root/ /root/.oh-my-zsh.zip && rm /root/.oh-my-zsh.zip

COPY ./src/.zshrc /root/

COPY ./src/mirrorlist /etc/pacman.d/

RUN pip install numpy scipy matplotlib scikit-learn scikit-image opencv-python jupyter tqdm \
    && pip install torch torchvision --extra-index-url https://download.pytorch.org/whl/cu116 \
    && pip config set global.index-url https://pypi.tuna.tsinghua.edu.cn/simple

COPY ./src/jupyter_notebook_config.py /root/.jupyter/
COPY ./src/start.sh /root

RUN echo "root:scnu" | chpasswd

WORKDIR /root/

CMD sh /root/start.sh