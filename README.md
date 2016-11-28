# docker-gpu-spark-keras-hyperopt-hyperas-elephas

Goal: Create a docker hosted GPU spark cluster that can do hyper paramater search on keras models. 

## Host machine setup

I selected an ubuntu 14.04 AMI from ec2. The steps to get the HOST docker machine running
Login to a GPU ec2 instance

```
wget https://developer.nvidia.com/compute/cuda/8.0/prod/local_installers/cuda-repo-ubuntu1404-8-0-local_8.0.44-1_amd64-deb
```

```
mv cuda-repo-ubuntu1404-8-0-local_8.0.44-1_amd64-deb
```

```
dpkg -i ./cuda-repo-ubuntu1404-8-0-local_8.0.44-1_amd64.deb
```

```
sudo apt-get update
```

```
sudo apt-get install cuda
```

```
sudo apt-get install linux-headers-$(uname -r)
```

```
sudo apt-get update
```

```
Sudo apt-get install nvidia-367
```

```
nvidia-modprobe
```

```
wget -qO- https://get.docker.com/ | sh
```

```
sudo usermod -aG docker $(whoami)
```

Log out and back in

```
wget -P /tmp https://github.com/NVIDIA/nvidia-docker/releases/download/v1.0.0-rc.3/nvidia-docker_1.0.0.rc.3-1_amd64.deb
```
```
sudo dpkg -i /tmp/nvidia-docker*.deb && rm /tmp/nvidia-docker*.deb
```
```
cd dockerbuild
```
```
nvidia-docker build -t mjk/gpu-spark-elephas .
```
```
nvidia-docker run -ti --rm mjk/gpu-spark-elephas nvidia-smi
```

Output here is running from inside the docker container

```
Fri Nov 25 03:08:25 2016       
+-----------------------------------------------------------------------------+
| NVIDIA-SMI 367.57                 Driver Version: 367.57                    |
|-------------------------------+----------------------+----------------------+
| GPU  Name        Persistence-M| Bus-Id        Disp.A | Volatile Uncorr. ECC |
| Fan  Temp  Perf  Pwr:Usage/Cap|         Memory-Usage | GPU-Util  Compute M. |
|===============================+======================+======================|
|   0  GRID K520           Off  | 0000:00:03.0     Off |                  N/A |
| N/A   26C    P8    18W / 125W |      0MiB /  4036MiB |      0%      Default |
+-------------------------------+----------------------+----------------------+

+-----------------------------------------------------------------------------+
| Processes:                                                       GPU Memory |
|  GPU       PID  Type  Process name                               Usage      |
|=============================================================================|
|  No running processes found                                                 |
+-----------------------------------------------------------------------------+
```
