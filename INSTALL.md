# Installation

To run these notebooks, there's **no need to install anything**: you can just run them in your browser, using Google Colab:

- <a href="https://colab.research.google.com/github/ageron/handson-mlp/blob/main/" target="_parent"><img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open In Colab"/></a> (recommended)

Other platforms like Kaggle or Binder should work as well.

However, if you really want to run these notebooks on your own machine, then please follow the instructions below.

> NOTE: Alternatively, you can [run these notebooks in a docker container](https://github.com/ageron/handson-mlp/blob/main/docker/README.md).

## Step 1, ensure you have uv and git
Make sure you have [uv](https://docs.astral.sh/uv/getting-started/installation) and [git](https://git-scm.com/downloads) installed:

You can use another Python package manager if you know what you are doing, but I've found `uv` to be very fast and simple to use, so I recommend it.

## Step 2, install the project and its dependencies
Let's download the `handson-mlp` project into your home directory, install all the required Python libraries into a new virtual environment (venv), and make this environment the default for Jupyter notebooks. Open a terminal and run:

```shell
cd  # goes to your home directory
git clone https://github.com/ageron/handson-mlp.git
cd handson-mlp
uv sync --frozen  # installs all the required Python libraries

# On MacOS or Linux
source .venv/bin/activate

# On Windows using the Command Prompt (cmd.exe)
.venv\Scripts\activate.bat

# On Windows using the PowerShell
.venv\Scripts\Activate.ps1

python -m ipykernel install --user --name=python3  # make this the default
```

If you get an error when activating the virtual environment in PowerShell, you may need to tweak the execution policy to allow PowerShell to execute scripts (this only applies to this terminal Window):
 
```powershell
Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass
```

## Step 3, select a GPU-enabled PyTorch build if needed
If you have an Nvidia GPU, make sure its driver is properly installed (please see your GPU manufacturer's instructions for more details). You do not need to replace PyTorch just because a GPU is present; first check whether the installed build already supports your hardware.

To select a different CUDA build, keep the compatibility bounds from `pyproject.toml`. The command below asks uv to resolve a compatible PyTorch family before replacing the installed packages, rather than uninstalling a working environment first:

```shell
cd
cd handson-mlp
source .venv/bin/activate  # on Windows, replace with same command as in step 2

# For an Nvidia CUDA 12.9 GPU (for other CUDA platforms, replace cu129 as needed)
uv pip install --torch-backend cu129 --reinstall-package torch --reinstall-package torchvision --reinstall-package torchaudio "torch>=2.8.0,<3.0.0" "torchvision>=0.23.0,<0.27.0" "torchaudio>=2.8.0,<3.0.0"
```

A later `uv sync --frozen` restores the lockfile's PyTorch builds, so reapply the CUDA selection afterward if needed.

**NOTE**: If you have a MacBook with MPS support ([Metal Performance Shaders](https://developer.apple.com/documentation/metalperformanceshaders)) then you don't need to upgrade the PyTorch libraries, as the default versions support MPS out of the box.

## How to start and stop the Jupyter Notebook server
Every time you want to start the Jupyter Notebook server, open a terminal and run:

```shell
cd
cd handson-mlp
source .venv/bin/activate  # on Windows, replace with same command as in step 2
jupyter notebook
```

To stop the server, press Ctrl-C in the terminal window (be sure to save your changes first).


## Optional softwares and libraries

You can optionally install the following softwares as well:

* [ffmpeg](https://www.ffmpeg.org/download.html): used in the Matplotlib tutorial, if you want to export an animation as an .mp4 video.
* [imagemagick](https://imagemagick.org/): used in the Matplotlib tutorial, if you want to export an animation as a .gif file.
* [graphviz](https://graphviz.org/): used in Chapter 5 if you want to generate an image from a .dot file.

You may also want to install the Box2D library, which is needed for a couple of exercises in Chapter 19, to load the LunarLander-v2 and BipedalWalker-v3 environments. You can generally install it by opening a terminal and running:

```shell
cd
cd handson-mlp
source .venv/bin/activate  # on Windows, replace with same command as in step 2
uv sync --extra box2d
```

This should work on most platforms. However, if you get an error, then it most likely means that the binary for your platform is not available, so you must build this library from the source code. For this, you first need to ensure that you have the essential tools for building a C++ project. For example, on Debian and Ubuntu you can open a terminal and run:

```shell
apt update && apt install -y build-essential cmake
```

Then you can install the `box2d-py` package (not `box2d`) from source:

```shell
cd
cd handson-mlp
source .venv/bin/activate  # on Windows, replace with same command as in step 2
uv add swig
uv add box2d-py
```

For Appendix B, `uv sync --extra quantization` installs `bitsandbytes` and
`gguf`. Availability of quantization features depends on your hardware and
platform. For Chapter 19's legacy Anaconda Atari setup,
`uv sync --extra legacy-atari` installs `AutoROM`. These extras are optional; you can combine
them by passing multiple `--extra` options.

Appendix E's `causal-conv1d` and `mamba-ssm` packages still require the manual
CUDA installation described in that notebook. Its prebuilt `cp312` wheels
are specific to Python 3.12 and cannot be used with Python 3.13.

## Update this project and its libraries

I regularly update the notebooks to fix issues and add support for the latest library versions. So make sure you update this project regularly.

For this, open a terminal, and run:

```shell
cd
cd handson-mlp
git pull
```

If you get an error, it's probably because you modified a notebook. In this case, before running `git pull` you will first need to commit your changes. I recommend doing this in your own branch, or else you may get conflicts:

```shell
git checkout -b my_branch # you can use another branch name if you want
git add -u
git commit -m "describe your changes here"
git checkout main
git pull
```

Next, let's update the libraries:

```shell
cd
cd handson-mlp
source .venv/bin/activate  # on Windows, replace with same command as in step 2
uv sync --frozen
```

Restart the Jupyter Notebook server (it may not be required, but it's safer).

That's it, have fun!
