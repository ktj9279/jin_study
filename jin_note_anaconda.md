# Anaconda


The open-source Anaconda Distribution is the easiest way to perform Python/R data science and machine learning on Linux, Windows, and Mac OS X. With over 11 million users worldwide, it is the industry standard for developing, testing, and training on a single machine, enabling individual data scientists to:


* Quickly download 1,500+ Python/R data science packages
* Manage libraries, dependencies, and environments with Conda
* Develop and train machine learning and deep learning models with scikit-learn, TensorFlow, and Theano
* Analyze data with scalability and performance with Dask, NumPy, pandas, and Numba
* Visualize results with Matplotlib, Bokeh, Datashader, and Holoviews


* References
    * [Anaconda](https://www.anaconda.com)
    * [Anaconda Cloud](https://anaconda.org/)
    * Anaconda > [Documentation](https://docs.anaconda.com/anaconda/)
    * Anaconda > [Anaconda Cheat Sheet](https://docs.anaconda.com/_downloads/9ee215ff15fde24bf01791d719084950/Anaconda-Starter-Guide.pdf)
    * [Conda](https://docs.conda.io/projects/conda/en/latest/index.html)
    * Conda > [Conda Cheat Sheet](https://docs.conda.io/projects/conda/en/latest/_downloads/1f5ecf5a87b1c1a8aaf5a7ab8a7a0ff7/conda-cheatsheet.pdf)
    * Conda > Docs > User guide > [Configuration](https://docs.conda.io/projects/conda/en/latest/user-guide/configuration/index.html)


Anaconda의 주요 기능이자 가장 큰 장점은 Python packages 간의 dependency 관리 및 가상환경이다. 뿐만 아니라, NVIDIA GPU를 기반으로 TensorFlow를 사용하기 위해서는 NVIDIA CUDA 관련 도구(CUDA Toolkit, cuDNN 등)가 필요하지만, Anaconda를 통해서 `tensorflow-gpu`를 설치할 경우 필요한 추가도구의 설치와 환경설정을 자동으로 해준다. TensorFlow가 권장하는 Docker는 Linux에서 최적화가 되어 있으므로, Windows 사용자로서는 Anaconda가 최선의 선택이라고 생각한다.


---


## Install Miniconda and Create Environments for Python 3.7


* Version: Miniconda 2019.07 (Conda 4.7.10 → 4.7.12)


정했습니다! 앞으로는 Miniconda만 쓰기로! Anaconda는 계속 이런저런 문제가 발생하네요...


* References
    * [Anaconda](https://www.anaconda.com/distribution/)
    * Anaconda > Documentation > Anaconda Distribution > [Installation](https://docs.anaconda.com/anaconda/install/)
    * [Miniconda](https://docs.conda.io/en/latest/miniconda.html)


* Environment and requirements
    * Windows 10 (64 bit)
    * NVIDIA driver 436.02


> 1. Install Miniconda [(Installing on Windows)](https://docs.anaconda.com/anaconda/install/windows/)


※ Anaconda Prompt를 실행하기 전에 속성에 들어가서 `시작 위치`를 본인의 workspace로 설정하면, 켤 때마다 매번 이동해야 하는 번거로움을 덜 수 있다.


> 2. Conda 및 root(base) environment의 기본 packages 업데이트


```bash
conda update conda
conda update --all
```


> 3. Create a new environment for Python 3.7


```bash
conda create -n python3.7 python
```


> 4. 필요한 packages 설치 및 Python base 환경 구축


```bash
conda create -n jin_python3.7_base --clone python3.7
conda activate jin_python3.7_base

# Install essential packages with h5py and hdf5.
conda install jupyter jupyterlab
conda install numpy scipy pandas xlrd
conda install matplotlib seaborn pillow
conda install scikit-learn scikit-image

# Others
conda install pywin32
conda install beautifulsoup4
conda install markdown
# conda install numba

# Install Node.js and JupyterLab extension for ipywidgets.
conda install -c conda-forge nodejs
jupyter labextension install @jupyter-widgets/jupyterlab-manager
jupyter lab build

# Install OpenCV.
conda install -c conda-forge opencv

# Install packages for medical imaging.
conda install -c conda-forge pydicom nibabel
conda install -c simpleitk simpleitk

# Install version_information.
conda install -c conda-forge version_information

conda deactivate
```


> 5. TensorFlow (with GPU Support) 설치 및 환경 구축


```bash
conda create -n jin_tensorflow1.14_base --clone jin_python3.7_base
conda activate jin_tensorflow1.14_base

# Install TensorFlow
conda install tensorflow-gpu

conda deactivate

conda create -n jin_tensorflow1.14 --clone jin_tensorflow1.14_base
```


---


## Install Anaconda and Create Environments for Python 3.7


* Version: Anaconda 2019.07 (Conda 4.7.10 → 4.7.11)


* References
    * [Anaconda Distribution](https://www.anaconda.com/distribution/)
    * Anaconda > Documentation > Anaconda Distribution > [Installation](https://docs.anaconda.com/anaconda/install/)


* Environment and requirements
    * Windows 10 (64 bit)
    * NVIDIA driver 436.02


> 1. Install Anaconda [(Installing on Windows)](https://docs.anaconda.com/anaconda/install/windows/)


> 2. Update `conda` ~~(Conda 및 root(base) environment의 기본 packages 업데이트)~~


```bash
conda update conda
# conda update --all
```


> 3. Create a new environment for Python 3.7


```bash
conda create -n python3.7 anaconda
```


> 4. 필요한 packages 설치 및 Python base 환경 구축


```bash
conda create -n jin_python3.7_base --clone python3.7
conda activate jin_python3.7_base

# ISSUE: conda 4.7.11 and hdf5
conda remove hdf5

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

conda deactivate
```


> 5. TensorFlow (with GPU Support) 설치 및 환경 구축


```bash
conda create -n jin_tensorflow1.14_base --clone jin_python3.7_base
conda activate jin_tensorflow1.14_base

# Install TensorFlow
conda install tensorflow-gpu

conda deactivate

conda create -n jin_tensorflow1.14 --clone jin_tensorflow1.14_base
```


---


## Install Anaconda and Create Environments for Python 3.6


* Version: Anaconda 2019.03 (Conda 4.7.5)


2019년 6월 25일 현재, Anaconda Distribution의 최신 버전은 Python 3.7을 기반으로 한다. 그러나 TensorFlow 1.13과 Keras 2.24는 Python 3.7과 호환이 안 되므로, Anaconda Documentation에서 권장하는 방법을 사용하여 Anaconda 설치 및 Python 3.6 environment를 구축하였다.


※ 이 문서를 정리한 뒤 이틀인가 삼일만에 TensorFlow 1.13부터 Python 3.7과 호환된다고 공식문서가 업데이트 되었다. Keras를 별도로 설치할 계획이 아니라 `tensorflow.keras`를 사용할 예정이라면 다운그레이드 할 필요 없이 Python 3.7을 그대로 사용하면 된다.


* `conda` 자동 업데이트 끄기


Conda 4.7.5 업데이트 후 여러 가지 문제가 발생하였다. 4.6.14일 때는 업데이트 해주던 packages를 최신 버전이라고 무시해버리거나, `conda update` 또는 `conda install` 시 대다수의 packages를 지워버리려고 한다. Root environment의 Python 버전을 3.6으로 다운그레이드 할 시에도 위와 같은 문제들이 발생하거나 아예 안 된다. GitHub에 여러 이슈들이 올라오는 중인것 같은데, 어차피 TensorFlow 1.14가 곧 업데이트 될 것 같으니 당분간 기다려보려고 한다. 다른 packages 설치 또는 업데이트 시 Conda도 자동 업데이트가 되는데, `conda config`로 자동 업데이트를 끌 수 있으며 `conda update conda` 또는 `conda update --all`을 하지 않는 이상 Conda가 자동으로 업데이트 되지 않는다.


```bash
conda config --set auto_update_conda False
```


※ [Why We Removed the “Free” Channel in Conda 4.7](https://www.anaconda.com/why-we-removed-the-free-channel-in-conda-4-7/)


* References
    * [Anaconda Distribution](https://www.anaconda.com/distribution/)
    * Anaconda > Documentation > Anaconda Distribution > [Installation](https://docs.anaconda.com/anaconda/install/)
    * Anaconda > Documentation > [FAQ > How do I get Anaconda with Python 3.5 or 3.6?](https://docs.anaconda.com/anaconda/user-guide/faq/#getting-anaconda)
    * Conda > Docs > User guide > Tasks > [Managing Python](https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-python.html)


* Environment and requirements
    * Windows 10 (64 bit)
    * NVIDIA driver 425.25
  

> 1. Install Anaconda [(Installing on Windows)](https://docs.anaconda.com/anaconda/install/windows/)


> 2. Update `conda` ~~(Conda 및 root(base) environment의 기본 packages 업데이트)~~


```bash
conda update conda
# conda update --all
```


> 3. Create a new environment for Python 3.6


Anaconda Documentation > FAQ > [Getting Anaconda](https://docs.anaconda.com/anaconda/user-guide/faq/#getting-anaconda) > 'How do I get Anaconda with Python 3.5 or 3.6?'을 보면 세 가지 방법을 제시한다.


> * 최신 버전의 Anaconda를 설치한 후 원하는 버전의 Python environment를 구축한다. (권장)


```bash
conda create -n python3.6 python=3.6 anaconda
```


or


> * 최신 버전의 Anaconda를 설치한 후 아래 명령어를 실행하여 root environment에 원하는 버전의 Python을 설치한다.


```bash
conda install python=3.6
```


※ Conda 4.6.14까지는 위 방법(root environment의 Python 버전을 다운그레이드)을 사용해도 좋다.


or


> * [Archive](https://repo.anaconda.com/archive/)에서 원하는 버전의 Python이 포함된 가장 최근 버전의 Anaconda installer를 다운로드하여 설치한다.


> 4. 필요한 packages 설치 및 Python base 환경 구축


```bash
conda create -n jin_python3.6_base --clone python3.6
conda activate jin_python3.6_base

# ISSUE: conda 4.7.11 and hdf5
conda remove hdf5

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

conda deactivate
```


> 5. TensorFlow (with GPU Support) 설치 및 환경 구축


```bash
conda create -n jin_tensorflow1.13_base --clone jin_python3.6_base
conda activate jin_tensorflow1.13_base

# Install TensorFlow
conda install tensorflow-gpu

conda deactivate

conda create -n jin_tensorflow1.13 --clone jin_tensorflow1.13_base
```


---


## Package 설치를 위한 팁


* [Anaconda Cloud](https://anaconda.org/)에서 package를 검색하여 채널 및 package의 버전을 확인하자.
    * Anaconda Documentation > Anaconda Distribution > Tasks > [Using default repositories](http://docs.anaconda.com/anaconda/user-guide/tasks/using-repositories/?highlight=default%20channel)
    * `conda install`
        * `-c`, `--channel`: Additional channel to search for packages.


* `conda install` vs. `pip install`
    * Anaconda로 설치 가능한 package는 `conda install` 명령어로 설치한다.
    * 그렇지 않다면, `pip install` 명령어를 통해 package installer for Python(pip)으로 설치한다.
        * Package installer for Python (pip)
        * [Python Package Index (PyPI)](https://pypi.org/)


* 설치 또는 업데이트 시 어떤 packages가 다운로드 및 설치되는지, dependency에 의해 관련 packages가 어떻게 변경되는지 반드시 확인할 것!


---


## Install Keras


### Install TensorFlow with GPU Support


* Version: TensorFlow 1.11.0


* References
    * TensorFlow > [Install](https://www.tensorflow.org/install)
    * TensorFlow > Install > [GPU support](https://www.tensorflow.org/install/gpu)
    * TensorFlow > Install > Build from source > Windows > [Tested build configurations](https://www.tensorflow.org/install/source_windows)
    * TensorFlow > Install > Build from source > Linux / max OS > [Tested build configurations](https://www.tensorflow.org/install/source#tested_build_configurations)


* Environment and requirements
    *  [NVIDIA® GPU drivers](https://www.nvidia.com/Download/index.aspx?lang=en-us)


TensorFlow와 Python 호환 버전은 reference로 달아놓은 'Tested build configurations'에서 확인하면 된다. 그러나 TensorFlow와 Keras의 호환 버전은 따로 알려주지 않기 때문에 직접 찾아야 한다. TensorFlow high-level API인 `tensorflow.keras`(TensorFlow's implementation of the Keras API specification)를 사용할 예정이라면 별도로 Keras를 설치할 필요가 없으며, Keras 버전과의 호환여부와 관계 없이 최신버전의 TensorFlow를 설치하면 된다.


> 1. Keras GitHub > [Releases](https://github.com/keras-team/keras/releases) > 설치하려는 Keras 버전의 release 날짜 확인


> 2. TensorFlow GitHub > [Releases](https://github.com/tensorflow/tensorflow/releases) > 1에서 확인한 Keras 버전보다 앞서 release된 TensorFlow 버전 확인
   

GPU가 지원되는 TensorFlow 버전과 채널을 확인한 후 설치한다.


> 3. [Anaconda Cloud](https://anaconda.org/) > `tensorflow-gpu` 검색
 

> 4. Anaconda Cloud에 있는 `tensorflow-gpu` package 중 2에서 확인한 버전과 비교하여 같은 버전 또는 이전 버전으로 설치


```bash
conda install tensorflow-gpu=1.11.0
```


### Install Keras


* Version: Keras 2.2.4


* References
    * Keras Documentation > [Installation](https://keras.io/#installation)


* Environment and requirements
    * Keras는 TensorFlow(default & 권장), Theano, CNTK 중 하나를 backend engine으로 사용하므로, Keras를 설치하기 전에 셋 중 하나를 설치해야 한다. 
    * Optional dependencies로 제시하는 것 중 다음 두 가지를 확인하자. (앞선 과정을 모두 `conda` 명령어로 진행했다면 두 가지 모두 자동으로 설치되었을 것이다.)
        * `cuDNN` (recommended if you plan on running Keras on GPU).
        * `HDF5` and `h5py` (required if you plan on saving Keras models to disk).


> Keras 설치


```bash
conda install keras
```


---


## Install Other Packages


[Anaconda Cloud](https://anaconda.org/)에서 설치하려는 package를 검색하여 버전 및 채널을 확인한 후 설치하자.


### [OpenCV](https://opencv.org/)


* Version: OpenCV 3.4.2


> OpenCV 설치


```bash
conda install opencv
```


or


```bash
# Linux user should use it.
conda install -c conda-forge opencv
```


### [pydicom](https://pydicom.github.io/pydicom/stable/index.html)


* Version: 1.3.0


> 설치


```bash
conda install -c conda-forge pydicom
```


or


```bash
pip install pydicom
```


### [NiBabel](https://nipy.org/nibabel/index.html#)


* Version: NiBabel 2.5.0


> NiBabel 설치


```bash
conda install -c conda-forge nibabel
```


or


```bash
pip install nibabel
```


### [SimpleITK](http://www.simpleitk.org/)


* Version: SimpleITK 1.2.2


> SimpleITK 설치


```bash
conda install -c conda-forge simpleitk
```


### [version_information](https://pypi.org/project/version_information/)


* Version: version_information 1.0.3


> version_information 설치


```bash
conda install -c conda-forge version_information
```


or


```bash
pip install version_information
```