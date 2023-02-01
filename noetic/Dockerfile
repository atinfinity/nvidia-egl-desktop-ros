FROM ghcr.io/selkies-project/nvidia-egl-desktop:20.04

SHELL ["/bin/bash", "-c"]
ENV DEBIAN_FRONTEND noninteractive
RUN sudo apt-get update && sudo apt-get install -y --no-install-recommends \
        curl \
        gnupg \
        lsb-release \
        less \
        emacs \
        tmux \
        bash-completion \
        command-not-found \
        software-properties-common \
        xdg-user-dirs \
        && \
    sudo apt-get clean && \
    sudo rm -rf /var/lib/apt/lists/*

# install ROS Noetic
RUN sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'
RUN curl -s https://raw.githubusercontent.com/ros/rosdistro/master/ros.asc | sudo apt-key add -
RUN sudo apt-get update && sudo apt-get install -y --no-install-recommends \
        ros-noetic-desktop-full \
        && \
    sudo apt-get clean && \
    sudo rm -rf /var/lib/apt/lists/*
RUN echo "source /opt/ros/noetic/setup.bash" >> ~/.bashrc

# dependencies for building packages
RUN sudo apt-get update && sudo apt-get install -y --no-install-recommends \
        python3-rosdep \
        python3-rosinstall \
        python3-rosinstall-generator \
        python3-wstool \
        build-essential \
        && \
    sudo apt-get clean && \
    sudo rm -rf /var/lib/apt/lists/*

# initialize rosdep
RUN sudo rosdep init && \
    rosdep update

# disabled beep sound
RUN echo "set bell-style none" >> ~/.inputrc

RUN sudo rm /etc/apt/apt.conf.d/docker-clean
