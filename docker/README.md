# Hands-On Machine Learning in Docker

If you would like to run and tweak the book's notebooks in a Docker container, you're in the right place!

## Prerequisites

You must first [Install Docker](https://docs.docker.com/engine/installation/).

If you have an Nvidia GPU and you're on Linux (or [WSL on Windows](https://learn.microsoft.com/en-us/windows/wsl/install)), then you can use your GPU inside the Docker container. For this, you must ensure that you have the [latest drivers for your GPU](https://www.nvidia.com/drivers/), and install the [Nvidia Container Toolkit[(https://github.com/NVIDIA/nvidia-container-toolkit) so Docker can access the GPU.

Below, I will assume that your Docker setup is functional and supports your GPU (if any).

## Usage

You can either download one of the images that I built and uploaded to docker.io, or you can build your own (that's slower but you get a fully up-to-date Docker image).

### Download an existing image

Choose the appropriate image, depending on your platform.

```bash
# CPU only
docker pull ageron/handson-mlp:cpu

# Nvidia GPU with CUDA 12.6 compute platform
docker pull ageron/handson-mlp:cu126
```

### Build your own image

Assuming you have already downloaded the project locally in your home folder:

```bash
cd  # go to your home folder
cd handson-mlp
docker build -t ageron/handson-mlp:cpu -f docker/Dockerfile --build-arg PT_VARIANT=cpu .
```

The build uses the checkout's `.python-version` and frozen lockfile without adding or removing project dependencies. Box2D is optional. To include Chapter 19's Box2D exercises, build with the declared `box2d` extra:

```bash
docker build -t ageron/handson-mlp:cpu-box2d -f docker/Dockerfile --build-arg PT_VARIANT=cpu --build-arg WITH_BOX2D=true .
```

If you want to build the Nvidia CUDA 12.6 variant, replace `cpu` with `cu126`. The CUDA installation keeps the PyTorch compatibility bounds declared in `pyproject.toml` while selecting backend-specific wheels. In the commands below, I'll use `cpu`, but you can replace `cpu` with the appropriate variant for your hardware.

> NOTE: You can see the list of available variants by visiting [PyTorch's download page](https://pytorch.org/get-started/locally/) and selecting Linux (even if you are on Windows or MacOS).

This will take quite a while and download gigabytes of data, but it is only required once.

After the process is finished you have an `ageron/handson-mlp:cpu` image (or `:cu126`): it will be the base for your experiments. You can confirm that by running the following command:

```bash
docker images
```

This should output something like this:

```
REPOSITORY            TAG         IMAGE ID            CREATED             SIZE
ageron/handson-mlp    cpu         3ebafebc604a        2 minutes ago       2.09GB
```

### Run the notebooks

Run the following commands to start the Jupyter server inside the container (which is named `homlp`):

```bash
cd  # go to the folder containing the handson-mlp directory
cd handson-mlp
docker run -it --rm --name homlp -p 8888:8888 -v "$PWD":/content ageron/handson-mlp:cpu
```

To run the optional Box2D image, replace `ageron/handson-mlp:cpu` with `ageron/handson-mlp:cpu-box2d` in the command above.

If you are using an Nvidia GPU, you must add `--gpus all` to the list of options.

Next, just point your browser to the URL printed on the screen (e.g., `http://127.0.0.1:8888/lab?token=ecaf97203325417dfe17e0824cb80e34cafcaa52e74485b0`), and you're ready to play with the book's code!

The project directory (in your home folder) is mapped to the `/content` directory inside the docker image. This means that the changes you make to the notebooks through the browser are saved in your project directory.

You can close the server by pressing `Ctrl-C` in the terminal window.

This will remove the container so you can start a new one later (but it will not remove the image or the notebooks, don't worry!).

Have fun!

