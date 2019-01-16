% Tensorflow-GPU in Docker
% Huang Yuefeng
% 2019.1.15
# Difference in docker installation
**without docker, we must install:**

  * Anaconda
  * pip install tensorflow-gpu
  * CUDA
  * cudnn
  * Nvidia Driver

**with docker, we need to install, and we can deploy it anywhere:**

  * Nvidia Driver
  * **docker**
  * Nvidia docker
  * Tensorflow-GPU image 

# Installation docker

  * Install Nvidia Driver

	```
	sudo apt-get purge nvidia driver-* cuda-* nvidia-docker2
	sudo add-apt-repository ppa:graphics-drivers/ppa
	sudo apt-get update
	sudo apt install nvidia-driver-410
	sudo reboot
	```

  * Install docker of corresponding version

	```
	sudo apt-get remove docker docker-engine docker.io containerd runc
	sudo apt-get update
	sudo apt-get install \
	    apt-transport-https \
	    ca-certificates \
	    curl \
	    gnupg2 \
	    software-properties-common
	curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
	sudo apt-key fingerprint 0EBFCD88
	sudo add-apt-repository \
	   "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
	   $(lsb_release -cs) \
	   stable"
	sudo apt-get update
	sudo apt-get install docker-ce=5:18.09.0~3-0~ubuntu-bionic	
	sudo docker container run hello-world
	```

---

  * Install Nvidia docker

	```
	docker volume ls -q -f driver=nvidia-docker | xargs -r -I{} -n1 docker ps -q -a -f volume={} | xargs -r docker rm -f
	sudo apt-get purge -y nvidia-docker
	curl -s -L https://nvidia.github.io/nvidia-docker/gpgkey | \
	sudo apt-key add - distribution=$(. /etc/os-release;echo $ID$VERSION_ID)
	curl -s -L https://nvidia.github.io/nvidia-docker/$distribution/nvidia-docker.list | \
  	sudo tee /etc/apt/sources.list.d/nvidia-docker.list
	sudo apt-get update
        sudo apt-get install -y nvidia-docker2
	sudo pkill -SIGHUP dockerd
	docker run --runtime=nvidia --rm nvidia/cuda:9.0-base nvidia-smi
	```

  * Get Tensorflow-GPU image 

        sudo docker pull tensorflow/tensorflow:latest-gpu
	sudo docker run --runtime=nvidia -it --rm tensorflow/tensorflow:latest-gpu python -c "import tensorflow as tf; tf.enable_eager_execution(); print(tf.reduce_sum(tf.random_normal([1000, 1000])))"

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
