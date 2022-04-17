# nvidia-egl-desktop-ros

## Introduction

This is a Dockerfile to use ROS on Ubuntu MATE Desktop container with NVIDIA GPU.  
This Dockerfile is based on [ehfd/docker-nvidia-egl-desktop](https://github.com/ehfd/docker-nvidia-egl-desktop).

![](nvidia-egl-desktop-ros-screenshot.png)

## Requirements

- NVIDIA graphics driver 450.80.02+ [^1]
- Docker
- nvidia-docker2

## Build docker image

### ROS Melodic

```
cd melodic
docker build -t nvidia-egl-desktop-ros:melodic .
```

### ROS Noetic

```
cd noetic
docker build -t nvidia-egl-desktop-ros:noetic .
```

## Launch docker container

Execute the command described below.  
If you customize setting, please read <https://github.com/ehfd/docker-nvidia-egl-desktop/blob/main/README.md>.

### ROS Melodic

```
docker run --gpus 0 -it --shm-size=1024m -e SIZEW=1920 -e SIZEH=1080 -e PASSWD=mypasswd -e BASIC_AUTH_PASSWORD=mypasswd -e NOVNC_ENABLE=true -p 6080:8080 nvidia-egl-desktop-ros:melodic
```

### ROS Noetic

```
docker run --gpus 0 -it --shm-size=1024m -e SIZEW=1920 -e SIZEH=1080 -e PASSWD=mypasswd -e BASIC_AUTH_PASSWORD=mypasswd -e NOVNC_ENABLE=true -p 6080:8080 nvidia-egl-desktop-ros:noetic
```

### Access Ubuntu MATE Desktop via web browser

Browse <http://127.0.0.1:6080/>.  
In this docker container, default account is `user`.  
You can set password via `PASSWD` and `BASIC_AUTH_PASSWORD` when you execute `docker run`. The default password is `mypasswd`.  

[^1]: <https://github.com/ehfd/docker-nvidia-egl-desktop/blob/main/README.md>