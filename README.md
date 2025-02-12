# Nerfstudio installation using conda
This guide explains how to setup nerfstudio with conda with a prexisting environment file (`environment.yml`).


## Install conda
Installing the latest miniconda since it's a lighter version of anaconda environment manager
```
curl https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh -o Miniconda3-latest-Linux-x86_64.sh
```
Make the installer executable and run it
```
chmod +x Miniconda3-latest-Linux-x86_64.sh
./Miniconda3-latest-Linux-x86_64.sh
```
Initialize conda for your current shell session
```
eval "$(/home/`<your_username>`/miniconda3/bin/conda shell.$(basename $SHELL) hook)"
```

Check conda installation
```
conda init
conda --version
```


## Create conda environment 
The conda environment for nerfstudio will be created via the `environment.yml` file with the following command
> **_NOTE:_**  `ffmpeg` is commented out from the installation, you might need to install it yourself for some commands

[Installing ffmpeg](#installing-ffmpeg)
```
conda env create -f environment.yml
```



When everything has been installed, activate the conda environment.
```
conda activate nerfstudio
```

## Setting up nerfstudio
### Install pytorch 
From the nerfstudio documentation, upgrading pip, checking that pytorch is not installed and installing pytorch with cuda support.
```
python -m pip install --upgrade pip

pip uninstall torch torchvision functorch tinycudann

pip install torch==2.1.2+cu118 torchvision==0.16.2+cu118 --extra-index-url https://download.pytorch.org/whl/cu118
```

Install necessary CUDA extensions from `cuda-toolkit` :
```
conda install -c "nvidia/label/cuda-11.8.0" cuda-toolkit
```

Install the torch bindings for `tiny-cuda-nn`:
```
pip install ninja git+https://github.com/NVlabs/tiny-cuda-nn/#subdirectory=bindings/torch
```

### Install nerfstudio from source


```
git clone https://github.com/nerfstudio-project/nerfstudio.git
cd nerfstudio
pip install --upgrade pip setuptools
pip install -e .
```

Optional tab completion for bash and zsh:
```
ns-install-cli
```

Check installation:
```
ns-train --help
```

## Installing ffmpeg
Use the following command to install `ffmpeg` through conda
```
conda install conda-forge::ffmpeg
```