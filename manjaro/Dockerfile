from manjarolinux/base:latest AS base

RUN pacman -Syyu --noconfirm & pacman -S --noconfirm cuda  & pacman -S --noconfirm python-pip & pacman -S --noconfirm openssh & pacman -Sc --noconfirm

RUN pip install  numpy scipy scikit-learn scikit-image opencv-python & pip3 install torch torchvision torchaudio --extra-index-url https://download.pytorch.org/whl/cu113

