FROM ghcr.io/ehfd/nvidia-egl-desktop:18.04

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

# install ROS Melodic
RUN sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'
RUN curl -s https://raw.githubusercontent.com/ros/rosdistro/master/ros.asc | sudo apt-key add -
RUN sudo apt-get update && sudo apt-get install -y --no-install-recommends \
        ros-melodic-desktop-full \
        && \
    sudo apt-get clean && \
    sudo rm -rf /var/lib/apt/lists/*
RUN echo "source /opt/ros/melodic/setup.bash" >> ~/.bashrc

# dependencies for building packages
RUN sudo apt-get update && sudo apt-get install -y --no-install-recommends \
        python-rosdep \
        python-rosinstall \
        python-rosinstall-generator \
        python-wstool \
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
