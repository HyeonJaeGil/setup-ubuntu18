# setup-ubuntu18
reference to what-to-install when using ubuntu18

## apt packages
```bash
sudo apt update && sudo apt upgrade -y
sudo apt install build-essential cmake pkg-config htop gedit wget git unzip curl vim software-properties-common libgtk2.0-dev ffmpeg libboost-all-dev apt-utils
```
## install korean
use ibus-setup
https://greedywyatt.tistory.com/105

## install browser
### whale
https://whale.naver.com/ko/download/linux/

## install ROS melodic
```bash
sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'
curl -s https://raw.githubusercontent.com/ros/rosdistro/master/ros.asc | sudo apt-key add -
sudo apt update
sudo apt install ros-melodic-desktop-full
echo "source /opt/ros/melodic/setup.bash" >> ~/.bashrc
source ~/.bashrc
sudo apt install python-rosdep python-rosinstall python-rosinstall-generator python-wstool build-essential
sudo apt install python-rosdep
sudo rosdep init
rosdep update
(below is optional)
sudo apt install python-catkin-tools
```

## install nvidia-driver, cuda
```bash
# nvidia driver 460
sudo apt install nvidia-driver-460
reboot
(check installation)
nvidia-smi

#cuda 11.2.2
wget https://developer.download.nvidia.com/compute/cuda/11.2.2/local_installers/cuda_11.2.2_460.32.03_linux.run
sudo sh cuda_11.2.2_460.32.03_linux.run
echo "export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/cuda-11.2/lib64" >> ~/.bashrc
echo "export PATH=$PATH:/usr/local/cuda-11.2/bin >> ~/.bashrc
source ~/.bashrc
```

## install docker, nvidia-docker
``` bash
# docker
sudo apt remove docker docker-engine docker.io containerd runc
sudo apt update
sudo apt install apt-transport-https ca-certificates gnupg lsb-release
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
echo "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt update
sudo apt install docker-ce docker-ce-cli containerd.io
sudo groupadd docker 
sudo usermod -aG docker $USER
docker run hello-world
sudo systemctl enable docker.service
sudo systemctl enable containerd.service

# nvidia-docker2
distribution=$(. /etc/os-release;echo $ID$VERSION_ID) \
   && curl -s -L https://nvidia.github.io/nvidia-docker/gpgkey | sudo apt-key add - \
   && curl -s -L https://nvidia.github.io/nvidia-docker/$distribution/nvidia-docker.list | sudo tee /etc/apt/sources.list.d/nvidia-docker.list
sudo apt-get update
sudo apt-get install -y nvidia-docker2
sudo systemctl restart docker
(check installation)
sudo docker run --rm --gpus all nvidia/cuda:11.0-base nvidia-smi

```
