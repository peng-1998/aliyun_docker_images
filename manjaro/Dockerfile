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

RUN pip config set global.index-url https://pypi.tuna.tsinghua.edu.cn/simple && pip install numpy scipy matplotlib scikit-learn scikit-image opencv-python jupyter && pip3 install torch torchvision torchaudio --extra-index-url https://download.pytorch.org/whl/cu113

COPY ./src/jupyter_notebook_config.py /root/.jupyter/

RUN echo "root:scnu" | chpasswd

WORKDIR /root/

CMD zsh