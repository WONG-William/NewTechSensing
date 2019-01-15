% Build Environment: Tensorflow-GPU in Docker
% Huang Yuefeng
% 2019.1.15
# Difference in docker installation
**without docker, we must install:**

  * Anaconda
  * pip install tensorflow-gpu
  * CUDA
  * cudnn
  * Nvidia Driver

**with docker, we just need to install:**

  * Nvidia Driver
  * **docker**
  * Nvidia docker
  * Tensorflow-GPU image 

# Installation docker

  * Disable ubuntu nouveau driver by

        sudo ubuntu-drivers autoinstall

  * Install docker of corresponding version

        sudo apt-get install docker-ce=18.09.0~ce~3-0~ubuntu

  * Install Nvidia docker

        sudo apt-get install -y nvidia-docker2

  * Get Tensorflow-GPU image 

        sudo docker pull tensorflow/tensorflow:devel-gpu

# Appendix
# Set Static IP for WiFi connected PC

```
network:
  version: 2
  renderer: NetworkManager
  ethernets:
    #network card identification
    wlx002127b8ee7a:
      dhcp4: no
      #IP/net mask by "ip a"
      addresses: [192.168.50.169/24]
      #gateway by "route -n"
      gateway4: 192.168.50.1
      nameservers:
        #use gateway as nameserver proxy by "nmcli dev show | grep DNS"
        addresses: [192.168.50.1]
```

# Docker Tips
```
docker pull
docker commit 
docker run -it
docker start
docker attach
docker rm
docker ps -a
docker cp
```
