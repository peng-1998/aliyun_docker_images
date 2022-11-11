from manjarolinux/base:latest
RUN pacman -Syyu --noconfirm \
    && pacman -S --noconfirm cuda python-pip zsh openssh unzip yay sudo curl\
    && pacman -Sc --noconfirm \
    && ssh-keygen -A

COPY ./src/sshd_config /etc/ssh/

# Install oh-my-zsh
RUN sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)" &&
    git clone https://github.com/zsh-users/zsh-autosuggestions ~/.oh-my-zsh/custom/plugins/zsh-autosuggestions &&
    git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ~/.oh-my-zsh/custom/plugins/zsh-syntax-highlighting &&
    sed -i 's/plugins=(git)/plugins=(git zsh-autosuggestions zsh-syntax-highlighting)/g' ~/.zshrc

COPY ./src/mirrorlist /etc/pacman.d/

RUN pip install numpy scipy matplotlib scikit-learn scikit-image opencv-python jupyter tqdm torch torchvision &&
    pip config set global.index-url http://172.17.0.1:9997/root/pypi/+simple/ &&
    pip config set install.trusted-host 172.17.0.1 &&
    echo "deb http://192.168.100.195:9998/ubuntu/ jammy main restricted universe multiverse" > /etc/apt/sources.list &&
    echo "deb http://192.168.100.195:9998/ubuntu/ jammy-updates main restricted universe multiverse" >> /etc/apt/sources.list &&
    echo "deb http://192.168.100.195:9998/ubuntu/ jammy-backports main restricted universe multiverse" >> /etc/apt/sources.list &&
    echo "deb http://192.168.100.195:9998/ubuntu/ jammy-security main restricted universe multiverse" >> /etc/apt/sources.list 


COPY ./src/jupyter_notebook_config.py /root/.jupyter/
COPY ./src/start.sh /root

RUN echo "root:scnu" | chpasswd

WORKDIR /root/

CMD sh /root/start.sh