from manjarolinux/base:latest AS base

RUN pacman -Syyu -unconfirm & pacman -S -unconfirm cuda  & pacman -S -unconfirm python-pip & pacman -S -unconfirm openssh & pacman -Sc -unconfirm

RUN pip install  numpy scipy scikit-learn scikit-image opencv-python & pip3 install torch torchvision torchaudio --extra-index-url https://download.pytorch.org/whl/cu113

