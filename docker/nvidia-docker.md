# nvidia-docker

Dockerfile

```bash
FROM nvidia/cuda:11.0-base-ubuntu20.04

ENV TZ=Asia/Taipei
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

# Install some basic utilities
RUN apt-get update && apt-get install -y \
    curl \
    ca-certificates \
    sudo \
    git \
    bzip2 \
    libx11-6 \
 && rm -rf /var/lib/apt/lists/*

RUN apt-get update -y && \
    apt-get install -y \
    libglib2.0-0 \
    libsm6 \
    libxext6 \
    libxrender-dev \
    libgl1-mesa-dev \
    git \
    # cleanup
    && apt-get autoremove -y \
    && apt-get clean -y \
    && rm -rf /var/lib/apt/li \
    && rm -rf /var/lib/apt/lists/*



# Create a working directory
RUN mkdir /app
WORKDIR /app

## Create a non-root user and switch to it
RUN adduser --disabled-password --gecos '' --shell /bin/bash user \
 && chown -R user:user /app
RUN echo "user ALL=(ALL) NOPASSWD:ALL" > /etc/sudoers.d/90-user
#USER user

# All users can use /home/user as their home directory
ENV HOME=/home/user
RUN chmod 777 /home/user

# Install Miniconda and Python 3.8
ENV CONDA_AUTO_UPDATE_CONDA=false
ENV PATH=/home/user/miniconda/bin:$PATH
RUN curl -sLo ~/miniconda.sh https://repo.continuum.io/miniconda/Miniconda3-py38_4.8.3-Linux-x86_64.sh \
 && chmod +x ~/miniconda.sh \
 && ~/miniconda.sh -b -p ~/miniconda \
 && rm ~/miniconda.sh \
 && conda install -y python==3.8.3 \
 && conda clean -ya

# CUDA 11.0-specific steps
RUN conda install -y -c pytorch \
    cudatoolkit=11.0.221 \
    "pytorch=1.7.0=py3.8_cuda11.0.221_cudnn8.0.3_0" \
    "torchvision=0.8.1=py38_cu110" \
 && conda clean -ya

RUN pip install scipy \
    numpy \
    Pillow \
    scikit-image \
    python-bidi \
    pyyaml

RUN pip install easyocr


# Set the default command to python3
CMD ["python3"]

```



啟動的時候記得要加上。

```bash
# device 要去看ubuntu上吃到的顯卡device為何？
docker run --gpus device=0 ....
```

### 安裝教學

安裝ＧＰＵ

```bash
 # 確定有沒有在
 sudo lshw -c display | grep NVIDIA
 
 # install gpu drive
 sudo Ubuntu-drivers devices
 sudo apt install nvidia-driver-450
 sudo reboot
 nvidia-smi
```

安裝docker-nvidia

```bash
# Docker
sudo apt-get update
sudo apt-get remove docker docker-engine docker.io
sudo apt install docker.io
sudo systemctl start docker
sudo systemctl enable docker
docker --version

# Put the user in the docker group
sudo usermod -a -G docker $USER
newgrp docker

# Nvidia Docker
sudo apt install curl
distribution=$(. /etc/os-release;echo $ID$VERSION_ID)
curl -s -L https://nvidia.github.io/nvidia-docker/gpgkey | sudo apt-key add -
curl -s -L https://nvidia.github.io/nvidia-docker/$distribution/nvidia-docker.list | sudo tee /etc/apt/sources.list.d/nvidia-docker.list

sudo apt-get update && sudo apt-get install -y nvidia-container-toolkit
sudo systemctl restart docker

```

```bash
# build and start docker
mkdir test
cd test
vim Dockerfile
mkdir tmp
docker build -t cuda11 .
docker run --gpus device=0 -it -v ./tmp cuda11 bash
# check yes or no
nvidia-smi 
```

```bash
conda env list
source activate base
##
python3
import torch
x = torch.rand(5, 3)
print(x)
```

```bash
# like this
tensor([[0.3380, 0.3845, 0.3217],
        [0.8337, 0.9050, 0.2650],
        [0.2979, 0.7141, 0.9069],
        [0.1449, 0.1132, 0.1375],
        [0.4675, 0.3947, 0.1426]])
```

