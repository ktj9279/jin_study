# Docker


Building and deploying new applications is faster with containers. Docker containers wrap up software and its dependencies into a standardized unit for software development that includes everything it needs to run: code, runtime, system tools and libraries. This guarantees that your application will always run the same and makes collaboration as simple as sharing a container image.


Docker containers whether Windows or Linux are backed by Docker tools and APIs and help you build better software:


* Onboard faster and stop wasting hours trying to set up development environments, spin up new instances and make copies of production code to run locally.
* Enable polyglot development and use any language, stack or tools without worry of application conflicts.
* Eliminate environment inconsistencies and the "works on my machine" problem by packaging the application, configs and dependencies into an isolated container.
* Alleviate concern over application security


* References
    * [Docker](https://www.docker.com/)
    * [Docker Documentation](https://docs.docker.com/)
    * Docker Documentation > Get started > [Get Started with Docker](https://docs.docker.com/get-started/)
    * Docker Documentation > Get started > [Docker overview](https://docs.docker.com/engine/docker-overview/)
    * [Docker glossary](https://docs.docker.com/glossary/?term=Dockerfile)
    * [Docker Hub](https://hub.docker.com/)
    * [시작하세요! 도커](https://wikibook.co.kr/docker/)
   
   
**Docker**: Docker is an open platform for developing, shipping, and running applications. Docker enables you to separate your applications from your infrastructure so you can deliver software quickly. With Docker, you can manage your infrastructure in the same ways you manage your applications.


* Linux container에 여러 기능을 추가함으로써 애플리케이션을 container로서 좀 더 쉽게 사용할 수 있게 만들어진 오픈소스 프로젝트
* 기존 가상화 방법인 가상 머신과는 달리 Docker container는 성능의 손실이 거의 없다.
* 일반적으로 Docker라 하면 Docker Engine 혹은 Docker에 관련된 모든 프로젝트를 의미한다.


**containerization**: The use of Linux containers to deploy applications is called containerization. Containers are not new, but their use for easily deploying applications is.


* Containers vs. Virtual Machines (VM)
    * A container **runs natively on Linux** and **shares the kernel of the host machine** with other containers. It runs a discrete process, **taking no more memory than any other executable**, making it **lightweight**.
    * By contrast, a virtual machine (VM) runs a full-blown **guest perating system (guest OS)** with virtual access to host resources through a **hypervisor**. In general, VMs provide an environment with more resources than most applications need.
        * 기존의 가상화 기술은 하나의 host OS 위에 여러 개의 guest OS를 생성하여 사용하는 방식
        * Guest OS는 hypervisor에 의해 생성되고 관리된다.
        * 각 guest OS는 완전히 독립적이다. (독립된 공감 및 시스템 자원을 할당받음.)
        * e.g. VirtualBox, VMware


<img src="./figures/Container@2x.png" alt="Docker Container" width="300"> <img src="./figures/VM@2x.png" alt="Virtual Machine" width="300">


---


## Docker Engine


**Docker Engine**: Docker Engine is a **client-server application**.


* Docker의 핵심으로, 컨테이너를 생성하고 관리하는 주체
* Major components
    * A **server** which is a type of long-running program called a **daemon** process (the `dockerd` command).
    * A **REST API** which specifies interfaces that programs can use to talk to the daemon and instruct it what to do.
    * A **command line interface (CLI) client** (the `docker` command).


<img src="./figures/engine-components-flow.png" alt="Docker Engine Components" width="500">


---


## Docker Architecture


Docker uses a **client-server architecture**. The Docker **client** talks to the Docker **daemon (server)**, which does the heavy lifting of building, running, and distributing your Docker containers. The Docker client and daemon can run on the same system, or you can connect a Docker client to a remote Docker daemon. The Docker client and daemon communicate using a REST API, over UNIX sockets or a network interface.


<img src="./figures/architecture.svg" alt="Docker Architecture" width="600">


**Docker daemon** (`dockered`): The Docker daemon **listens for Docker API requests** and **manages Docker objects** such as images, containers, networks, and volumes. A daemon can also communicate with other daemons to manage Docker services.


**Docker client** (`docker`): The Docker client is **the primary way that many Docker users interact with Docker**. When you use commands such as `docker run`, the client sends these commands to `dockerd`, which carries them out. The `docker` command uses the **Docker API**. The Docker client can communicate with more than one daemon.


**Docker registries**: A Docker registry **stores Docker images**.


**Docker Hub**: Docker Hub is a **public registry** that anyone can use, and Docker is configured to look for images on Docker Hub by default.


---


## Docker Objects


Images, containers, networks, volumes, plugins, and other objects


**Image**: A container is launched by running an image. An image is an **executable package** that includes everything needed to run an application--the code, a runtime, libraries, environment variables, and configuration files.


* An image is a **read-only template** with instructions for creating a Docker container.
    * 생성된 이미지는 어떠한 경우로도 변경되지 않는다. 컨테이너를 실행한 후 변경된 내용은 컨테이너 계층에 저장되며, 컨테이너 삭제 시 저장되어 있던 내용 또한 삭제된다.
* Often, an image is **based on another image**, with some additional customization.
    * e.g. Ubuntu image 위에 Python과 TensorFlow를 설치
* 직접 만들 수도 있고, 다른 사람이 만들어서 배포한 것을 사용할 수도 있다.
* To build your own image, you create a **Dockerfile** with a simple syntax for defining the steps needed to create the image and run it. Each instruction in a Dockerfile creates a layer in the image. When you change the Dockerfile and rebuild the image, only those layers which have changed are rebuilt (lightweight).
* Image 이름의 기본 형태 : `[저장소 이름]/[이미지 이름]:[태그]` e.g. `ktj9279/ubuntu:18.04` or `ubuntu:latest`
    * 저장소 이름 : 생략 가능. 저장소 이름이 별도로 명시되지 않은 이미지는 Docker Hub의 공식 이미지임을 뜻한다.
    * 태그 : 일반적으로 버전을 명시하여 버전 관리 혹은 리비전 관리에 사용된다. 생략 시 `latest`로 인식.
* Commit 할 때 추가 혹은 변경된 내용만 새로운 layers로 저장한 후 관련된 모든 layers를 포함하여 새로운 image를 만든다. 따라서 `docker images`를 했을 때 어떤 image의 크기가 100MB라고 출력될지라도 실제로는 100MB를 차지하는 것이 아니라 추가된 layers에 해당하는 용량만 차지하게 된다.


**Container**: A container is a **runtime instance of an image**--what the image becomes in memory when executed (that is, an image with state, or a user process).


* A container is a **runnable instance** of an image.
* You can create, start, stop, move, or delete a container using the Docker API or CLI.
* You can connect a container to one or more networks, attach storage to it, or even create a new image based on its current state.
* By default, a container is relatively well isolated from other containers and its host machine. 
* A container is defined by its image as well as any configuration options you provide to it when you create or start it. When a container is removed, any changes to its state that are not stored in persistent storage disappear.
* 하나의 이미지로 여러 개의 컨테이너(해당 이미지의 목적에 맞는 파일이 들어 있는 파일시스템과 격리된 시스템 자원 및 네트워크를 사용할 수 있는 독립된 공간)를 생성할 수 있다.
* 각 컨테이너에서 무엇을 하든지 다른 컨테이너, 이미지, 호스트는 영향을 받지 않는다.
* 가상 머신이 가상 IP 주소를 할당받는 것처럼, Docker는 container에 172.17.0.x의 IP(`ipconfig`로 확인 가능)를 순차적으로 할당한다. Container의 IP와 port를 host의 IP와 port에 바인딩해야만 외부에서 컨테이너 내부의 애플리케이션으로 접근이 가능하며, 아무런 설정을 하지 않았다면 해당 container는 host에서만 접근할 수 있다.
    * 컨테이너 내부의 애플리케이션이 어떤 port(e.g. 아파치 웹 서버는 기본적으로 80번 port를 사용)를 통해 서비스를 제공하는지 확인하여 해당 컨테이너 port를 호스트 port와 바인딩해야 한다.
* 여러 개의 애플리케이션을 한 컨테이너에 설치할 수도 있지만, 한 개의 컨테이너에 프로세스(애플리케이션) 하나만 실행하는 것이 Docker의 철학이다. 컨테이너 간의 독립성 보장, 애플리케이션 버전 관리, 소스코드 모듈화 등이 더욱 쉬워진다.
    * e.g. 분리된 애플리케이션 컨테이너 : 데이터베이스 컨테이너, 웹 서버 컨테이너


---


## Install Docker for Ubuntu


* Version: Docker CE 18.09.5


* References
    * [Get Docker CE for Ubuntu](https://docs.docker.com/install/linux/docker-ce/ubuntu/)


* Environment and requirements
    * Ubuntu 18.04 (LTS) (64-bit)


### Prerequisites


> 1. Check OS requirements.
>     * Linux kernel version and 64-bit (`x86_64`)
>         * 3.10 버전 이상이 필요
>     * root 권한을 가진 계정 또는 sudo 명령어로 설치


```bash
uname -a
```


> 2. Uninstall old versions.
>     * Older versions of Docker were called `docker`, `docker.io`, or `docker-engine`.
>     * The Docker CE package is now called `docker-ce`.


```bash
sudo apt-get remove docker docker-engine docker.io containerd runc
```


### [Set Up the Repository](https://docs.docker.com/install/linux/docker-ce/ubuntu/#install-using-the-repository)


Before you install Docker CE for the first time on a new host machine, you need to set up the Docker repository. Afterward, you can **install and update Docker from the repository**.


### Install Docker CE


> 1. Update the `apt` package index.


```bash
sudo apt-get update
```


> 2. Install the latest version of Docker CE and containerd.


```bash
sudo apt-get install docker-ce docker-ce-cli containerd.io
```


> 3. Verify that Docker CE is installed correctly.


```bash
docker version
```


### [Post-installation steps for Linux](https://docs.docker.com/install/linux/linux-postinstall/)


> 1. `sudo` 없이 `docker` 명령어를 사용할 수 있도록 `docker` 그룹에 사용자 추가


```bash
sudo usermod -aG docker USER
reboot
```
~~`gpasswd -a USER docker`~~


### Uninstall Docker CE


> 1. Uninstall the Docker CE package.


```bash
sudo apt-get purge docker-ce
```


> 2. Delete all images, containers, and volumes.


```bash
sudo rm -rf /var/lib/docker
```


> 3. Delete any edited configuration files manually.


---


## 자주 사용하는 Docker 명령어


> `docker info`, `docker version`, `docker -v` or `docker --version`: Show information and version.


> `docker images`: List images.


> `docker ps`: List containers (실행 중인 containers만 출력)
> * `-a`: 모든 containers 출력
> * `-q`: Container의 ID만 출력
> * COMMAND: Container가 시작될 때 실행될 명령어로, 대부분의 image에 미리 내장되어 있다.
> * STATUS: Container의 상태
>     * Up: 실행 중
>     * Exited: 종료
>     * Pause: 일시 중지
> * PORTS: Container가 개방한 port와 host에 연결한 port를 나열한다. Container 생성 시 외부에 노출하도록 설정하지 않을 경우 아무것도 출력되지 않는다.
> * NAMES: Container의 고유한 이름. Container 생성 시 `--name` 옵션으로 설정하지 않을 경우 임의로 형용사와 명사를 무작위로 조합하여 결정된다.


> `docker search`: Search the Docker Hub for images.


> `docker push`: Push an image or a repository to a registry.
> * `docker tag`: Create a tag TARGET_IMAGE that refers to SOURCE_IMAGE.
>     * 복사가 아니라 태그(별칭)만 붙여주는 것이다.
>     * Push를 하려면 이미지 이름 앞에 반드시 저장소 이름(Docker ID와 동일)을 붙여주어야 한다.
> * `docker login`: Push 또는 private repository의 image를 pull 하려면 로그인을 통한 권한 획득이 필요하다.
> * `docker logout`: 공용 컴퓨터일 경우 push 또는 pull을 마친 후 로그아웃 하자.


> `docker pull`: Pull an image or a repository from a registry.


> `docker create`: Create a new container.
> * Image가 local docker engine에 존재하지 않을 경우 Docker Hub에서 자동으로 pull.
> * Container ID(무작위 16진수 해시값)를 출력


```bash
docker create -it --name CONTAINER IMAGE:TAG
```


> `docker start`: Start one or more stopped containers.


> `docker attach`: Attach local standard input, output, and error streams to a running container.


> `docker commit`: Create a new image from a container's changes.
> * `-a`: Author
> * `-m`: Commit message


```bash
docker commit CONTAINER IMAGE:TAG
```


> `docker run`: Run a command in a new container. (container 생성 후 내부로 들어감.)  
= `docker pull` (image가 없을 경우) + `docker create` + `docker start` + `docker attach` (`-it` 옵션을 사용했을 때)
> * `-d`, `--detach`: Run container in background and print container ID.
>     * `-it`와 달리 입출력이 없는 상태(백그라운드)로 컨테이너를 실행한다.
>     * Detached 모드인 컨테이너는 반드시 포그라운드 프로그램이 실행돼야 하며, 그렇지 않으면 바로 컨테이너가 종료된다.
> * `-e`, `--env`: Set environment variables.
> * `-it`: Container와 상호(interactive) 입출력을 가능하게 함. 즉, bash shell을 사용하도록 설정.
>     * `-i`, `--interactive`: Keep STDIN open even if not attached.
>         * 상호 입출력 활성화
>     * `-t`, `--tty`: Allocate a pseudo-TTY.
>         * Teletype(tty) 활성화
> * `--link`: Add link to another container.
>     * 연결할 컨테이너의 IP를 알 필요 없이 별칭으로 접근하도록 설정
>     * 이때 실행 순서의 의존성이 생기는데, 연결할 컨테이너가 존재하지 않거나 실행 중이 아니라면 `--link`가 적용된 컨테이너 또한 실행할 수 없다.
> * `--name`: Assign a name to the container.
> * `-p`, `--publish`: Publish a container's port(s) to the host.
>     * Container의 port를 host의 port와 binding한다.
>     * Host의 특정 IP를 사용할 수 있다.
>         * `0.0.0.0`은 호스트의 활용 가능한 모든 네트워크 인터페이스에 바인딩 하는 것을 뜻한다.
>     * 나열하여 여러 개의 port를 외부에 개방할 수 있다.
> * `--rm`: Automatically remove the container when it exits.
> * `--runtime`: Runtime to use for this container.
> * `-v`, `--volume`: Bind mount a volume.
>     * 볼륨을 활용(아래 세 가지 방법 중 하나 선택)하여 컨테이너를 삭제해도 데이터가 보존되도록 한다.
>         * Host와 볼륨 공유 : Host의 디렉토리를 Container의 디렉토리에 mount
>         * 볼륨 컨테이너 활용
>         * Docker가 관리하는 볼륨을 생성
> * Image가 local docker engine에 존재하지 않을 경우 Docker Hub에서 자동으로 pull한다.
> * Container 내부에서 기본 사용자는 root, host 이름은 무작위의 16진수 해시값(container ID의 앞 일부분).


```bash
docker run -it --name CONTAINER IMAGE:TAG

docker run -it -p HOST_PORT:CONTAINER_PORT IMAGE:TAG
docker run -it -p HOST_IP:HOST_PORT:CONTAINER_PORT IMAGE:TAG 
docker run -it -p HOST_PORT:CONTAINER_PORT -p HOST_PORT:CONTAINER_PORT IMAGE:TAG

docker run --link CONTAINER_TO_LINK:ALIAS

docker run -v HOST_DIR:CONTAINER_DIR
```


> `docker exec`: Run a command in a running container
> * Detached 모드로 동작 중인 container의 `/bin/bash` 프로세스를 실행할 수 있다.


```bash
docker exec -it CONTAINER bash
```



> Container를 정지하고 내부에서 빠져나오는 방법


```bash
exit
```


or


```
Ctrl + D
```


> Container를 정지하지 않고 내부에서 빠져나오는 방법


```
Ctrl + P, Q
```


> `docker name`: Rename a container.


> `docker stop`: Stop one or more running containers.
> * `docker ps -a -q`와 함께 사용하여 한꺼번에 모든 containers를 종료할 수 있다.


```bash
docker stop $(docker ps -a -q)
```


> `docker rm`: Remove one or more containers.
> * 실행 중인 container는 삭제할 수 없으므로, 정지한 뒤 삭제하거나 `-f` 옵션을 사용한다.


> `docker rmi`: Remove one or more images.


---


## Install NVIDIA Docker for Ubuntu


* Version: NVIDIA Docker 2.0.3


* Environment and requirements
    * Ubuntu 18.04 (LTS)
    * NVIDIA driver 418.56
    * Docker 18.09.5 CE


* References
    * GitHub > [NVIDIA/nvidia-docker](https://github.com/NVIDIA/nvidia-docker)
    * GitHub > NVIDIA/nvidia-docker > [Documentation](https://github.com/NVIDIA/nvidia-docker/wiki)
    * NVIDIA > Developer > CUDA toolkit documentation > [NVIDIA CUDA Installation Guide for Linux](https://docs.nvidia.com/cuda/cuda-installation-guide-linux/index.html#package-manager-installation)
    * NVIDIA > Developer > [CUDA GPUs](https://developer.nvidia.com/cuda-gpus) (Types of product and compute capability = GPU architectures)
    * GitHub > NVIDIA/nvidia-docker > Documentation > ... > [CUDA](https://github.com/NVIDIA/nvidia-docker/wiki/CUDA#requirements) (CUDA toolkit versions, driver versions and GPU architectures)
    * WIKIPEDIA > [CUDA](https://en.wikipedia.org/wiki/CUDA)


<img src="./figures/nvidia_container_runtime_for_docker.png" alt="NVIDIA Container Runtime for Docker" width="500">


```bash
# If you have nvidia-docker 1.0 installed: we need to remove it and all existing GPU containers
docker volume ls -q -f driver=nvidia-docker | xargs -r -I{} -n1 docker ps -q -a -f volume={} | xargs -r docker rm -f
sudo apt-get purge -y nvidia-docker

# Add the package repositories
curl -s -L https://nvidia.github.io/nvidia-docker/gpgkey | \
  sudo apt-key add -
distribution=$(. /etc/os-release;echo $ID$VERSION_ID)
curl -s -L https://nvidia.github.io/nvidia-docker/$distribution/nvidia-docker.list | \
  sudo tee /etc/apt/sources.list.d/nvidia-docker.list
sudo apt-get update

# Install nvidia-docker2 and reload the Docker daemon configuration
sudo apt-get install -y nvidia-docker2
sudo pkill -SIGHUP dockerd

# Check the version of nvidia-docker
nvidia-docker version
```


※ NVIDIA Docker를 실행하는 두 가지 방법 (nvidia-docker v1 uses the `nvidia-docker` alias, where v2 uses `docker --runtime=nvidia`.)


```bash
docker run --runtime=nvidia
```


or


```bash
nvidia-docker run
```


---


## Pull NVIDIA CUDA and cuDNN images


* Version: `nvidia/cuda:10.0-cudnn7-devel-ubuntu16.04`


* References
    * Docker Hub > [nvidia/cuda](https://hub.docker.com/r/nvidia/cuda)


* Environment and requirements
    * Ubuntu 16.04 (LTS)
    * NVIDIA driver 435.21
    * Docker 18.06.1-ce
    * NVIDIA Docker 2.0.3


> 1. 컴퓨터에 설치된 GPU 및 NVIDIA driver와 호환되는 CUDA toolkit 버전을 확인한 후, Docker Hub에서 CUDA container images의 태그를 확인
>     * CUDA docker images are constrained by the Nvidia Driver and GPU of the host. See [nvidia-docker requirements](https://github.com/NVIDIA/nvidia-docker/wiki/CUDA#requirements) for more details. 


> 2. Pull the Docker image


```bash
docker pull nvidia/cuda:10.0-cudnn7-devel-ubuntu16.04
```


> 3. Container를 실행하여 CUDA toolkit의 버전을 확인


```bash
docker run --runtime=nvidia --rm nvidia/cuda:10.0-cudnn7-devel-ubuntu16.04 nvcc --version
```


---


## Install Miniconda for Python 3.7 using Docker


* Version: Miniconda 2019.07 (Conda 4.7.10)


* References
    * [Anaconda Distribution](https://www.anaconda.com/distribution/)
    * Anaconda > Documentation > Anaconda Distribution > [Installation](https://docs.anaconda.com/anaconda/install/)
    * [Miniconda](https://docs.conda.io/en/latest/miniconda.html)
    * ~~[How To Install Anaconda on Ubuntu 18.04 [Quickstart]](https://www.digitalocean.com/community/tutorials/how-to-install-anaconda-on-ubuntu-18-04-quickstart)~~
    * Docker Hub > [continuumio/anaconda3](https://hub.docker.com/r/continuumio/anaconda3)
    * Docker Hub > [continuumio/miniconda3](https://hub.docker.com/r/continuumio/miniconda3)


* Environment and requirements
    * Ubuntu 16.04 (LTS)
    * NVIDIA driver 435.21
    * Docker 18.06.1-ce
    * NVIDIA Docker 2.0.3
    * CUDA docker image: `nvidia/cuda:10.0-cudnn7-devel-ubuntu16.04`


> ~~1. Pull and run the official anaconda image.~~


~~docker pull continuumio/anaconda3~~
~~docker run -it continuumio/anaconda3~~


~~or~~


> 1. Download the Miniconda installer.


```bash
wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh
```


> 2. Run the CUDA docker image.


```bash
docker run --runtime=nvidia -it -v [Miniconda installer를 다운로드한 위치]:/tmp nvidia/cuda:10.0-cudnn7-devel-ubuntu16.04
```


> 3. Install Miniconda [(Installing on Linux)](https://docs.anaconda.com/anaconda/install/linux/).


> 4. Commit initial Miniconda image.


```bash
exit

docker commit CONTAINER ktj9279/miniconda:2019.07-py3.7

docker rm CONTAINER
```


> 5. Customize Miniconda environments and packages.


```bash
docker run --runtime=nvidia -it miniconda:2019.07-py3.7

# TODO: Customizing... (including installing TensorFlow)
conda update conda
conda update --all

# Install essential packages with h5py and hdf5.
# ISSUE: JupyterLab 1.0.2에서 labextension을 설정시 사이드바 및 탭 깨짐 현상 → conda-forge 채널에서 JupyterLab 1.1.3 설치
conda install -c conda-forge jupyter jupyterlab
conda install numpy scipy pandas
conda install matplotlib seaborn pillow
conda install scikit-learn scikit-image

# Others
conda install beautifulsoup4
conda install markdown
# conda install numba

# Install Node.js and JupyterLab extension for ipywidgets.
conda install -c conda-forge nodejs
jupyter labextension install @jupyter-widgets/jupyterlab-manager

# Install OpenCV.
conda install -c conda-forge opencv

# Install packages for medical imaging.
conda install -c conda-forge pydicom nibabel
conda install -c simpleitk simpleitk

# Install version_information.
conda install -c conda-forge version_information
```


> 6. Commit your Miniconda image.


```bash
exit

docker commit CONTAINER ktj9279/miniconda:2019.07-py3.7-jin

docker rm CONTAINER
```


---


## Install TensorFlow on Miniconda


* Version: TensorFlow 1.14.0 with GPU support


* Environment and requirements
    * Ubuntu 16.04 (LTS)
    * NVIDIA driver 435.21
    * Docker 18.06.1-ce
    * NVIDIA Docker 2.0.3
    * CUDA docker image: `nvidia/cuda:10.0-cudnn7-devel-ubuntu16.04`
    * Miniconda 2019.07
    * Python 3.7


> 1. Run your Miniconda image.


```bash
docker run --runtime=nvidia -it ktj9279/miniconda:2019.07-py3.7-jin
```


> 2. Install TensorFlow.


```bash
# Install TensorFlow with cudatoolkit, cudnn
conda install tensorflow-gpu
```


> 3. Commit TensorFlow image.


```bash
exit

docker commit CONTAINER ktj9279/miniconda:2019.07-py3.7-tf1.14.0gpu-jin

docker rm CONTAINER
```


※ ~~`nvidia/cuda` image의 버전과 Anaconda `cudatoolkit`의 버전을 동일하게 맞춘다.~~