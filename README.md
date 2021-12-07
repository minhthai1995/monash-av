## Installation Carla and Autoware
### Install CARLA:
Use this [link](https://github.com/carla-simulator/carla/releases/tag/0.9.10.1) to download CARLA 0.9.10.1 (CARLA_0.9.10.1.tar.gz)

```
tar xvzf CARLA_0.9.10.1.tar.gz
```
### Install Docker Engine on Ubuntu
```
sudo apt update
sudo apt install apt-transport-https ca-certificates curl software-properties-common
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu focal stable"
apt-cache policy docker-ce
sudo apt install docker-ce
```

### Install Nvidia Docker
```
distribution=$(. /etc/os-release;echo $ID$VERSION_ID) \
   && curl -s -L https://nvidia.github.io/nvidia-docker/gpgkey | sudo apt-key add - \
   && curl -s -L https://nvidia.github.io/nvidia-docker/$distribution/nvidia-docker.list | sudo tee /etc/apt/sources.list.d/nvidia-docker.list
curl -s -L https://nvidia.github.io/nvidia-container-runtime/experimental/$distribution/nvidia-container-runtime.list | sudo tee /etc/apt/sources.list.d/nvidia-container-runtime.list
sudo apt-get update
sudo apt-get install -y nvidia-docker2
sudo systemctl restart docker
```
### Setup the carla_autoware
Next, clone the carla autoware repository
```sh
git clone --recurse-submodules https://github.com/carla-simulator/carla-autoware
```
Build the image using:
```sh
cd carla-autoware && ./build.sh
```
This will generate a `carla-autoware:latest` docker image.

### Run the agent
1. Run a CARLA server.

```sh
./CarlaUE4.sh
```

2. Run the `carla-autoware` image: 

```sh
./run.sh
```

This will start an interactive shell inside the container. To start the agent run the following command:

```sh
roslaunch carla_autoware_agent carla_autoware_agent.launch town:=Town01
```
