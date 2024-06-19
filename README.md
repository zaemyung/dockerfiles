# Docker Cheat Sheet
(Adopted from [Docker Cheat Sheet](https://www.docker.com/sites/default/files/d8/2019-09/docker-cheat-sheet.pdf))
- You can also take a look at this [one](https://github.com/minnesotanlp/servers/blob/main/Docker_for_Beginners_Version_2_1680555182.pdf).
- Here is also a good [Docker tutorial](https://www.youtube.com/watch?v=pg19Z8LL06w) on YouTube.

## Build
Build an image from the Dockerfile in the current directory and tag the image, e.g.:
> `docker build -f Dockerfile -t zaemyung/ml:latest .`

For building `zaemyung/ml_zae` image (non-root image), pass `UNAME`, `UID`, and `GID` as:
> `docker build --build-arg UNAME={your_name} --build-arg UID=$(id -u) --build-arg GID=$(id -g) -f Dockerfile -t zaemyung/ml_zae .`

List all images that are locally stored with the Docker Engine
> `docker image ls`

Delete an image from the local image store
> `docker image rm zaemyung/cuda:12.1-python3.11`

For more info, refer to Docker [build](https://docs.docker.com/engine/reference/commandline/build/) and [image](https://docs.docker.com/engine/reference/commandline/image/) references

## Run
Run an interactive container from the latest version of `zaemyung/ml_zae` image; expose all GPUs to the container; name the running container "zaemyung-ml"; expose port 8888 externally and map to port 8888 inside the container; and map the host volume (`/space4/zaemyung/Development`) to container path (`/space4/zaemyung/Development`)
> `docker container run -it --gpus all --shm-size='1gb' --name zaemyung-ml -p 8888:8888 --volume /space4/zaemyung/Development:/space4/zaemyung/Development zaemyung/ml_zae:latest`

Show running containers
> `docker container ls`

Show all containers including the exited ones
> `docker container ls -a`

Stop a container
> `docker container stop {CONTAINER_NAME}`

Deleting a container
> `docker container rm {CONTAINER_NAME}`

Attach to a running container
> `docker container attach {CONTAINER_NAME}`

Detach from the container
> `ctrl-p, ctrl-q`

For more info, refer to Docker [run](https://docs.docker.com/engine/reference/run/) reference

## Share
Docker images can be shared via [Docker Hub](https://hub.docker.com) or [GitHub Packages](https://github.com/features/packages).

Retag a local image with a new image name and tag
> `docker tag myimage:1.0 myrepo/myimage:2.0`

Pull an image from a registry
> `docker pull myrepo/myimage:2.0` *(Docker Hub)*
>
> `docker pull ghcr.io/myrepo/myimage:2.0` *(GitHub Packages)*

Login to a registry
> `docker login --username {username} --password-stdin` *(Docker Hub)*
>
> `docker login ghcr.io --username {username} --password-stdin` *(GitHub Packages)*

Push an image to a registry
> `docker push myrepo/myimage:2.0` *(Docker Hub)*
>
> `docker push ghcr.io/myrepo/myimage:2.0` *(GitHub Packages)*

## Some info.
- [Installation guide for Docker](https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/install-guide.html#docker)
- To enable GPUs (CUDA) in the container, it is sufficient to install appropriate NVIDIA driver in the host machine.
  - The actual CUDA toolkit does not need to be installed in the host.
  - However, the version of the NVIDIA driver must be recent enough to support the CUDA version of the container.
  - To upgrade NVIDIA driver of host machine, check the necessary drive version in [CUDA Toolkit and Corresponding Driver Versions](https://docs.nvidia.com/cuda/cuda-toolkit-release-notes/index.html).
  - Then upgrade via: `sudo apt install nvidia-driver-{VERSION}` where `VERSION` could be `495` or so.
    - Afterward, `sudo reboot` is required.
- Both CUDA and NVIDIA Drivers are backward-compatible.
- When starting a container, `--gpus all` flag needs to be passed to expose GPUs to the container.
- It is recommended to write and build image from Dockerfile rather than installing softwares directly inside a container.
- By default, within the container, you are a root user. Should you wish to be a non-root user, you can take a look at [this dockerfile](https://github.com/zaemyung/dockerfiles/blob/master/ml_non_root/Dockerfile) and adopt it to your needs.
  - When building the image, you can pass your user ID and group ID by `docker build --build-arg UID=$(id -u) --build-arg GID=$(id -g) -f Dockerfile -t {your_name/repo_name:tag} .`

## Q&A
- How to install packages on Docker for a specific image?
  - A docker image is defined by a Dockerfile, so ideally, all the necessary packages and programs for your environment must be specified within the Dockerfile. However, it is also possible to install and add packages within the Docker container and later `commit` the changes as a new image. But the [former is generally recommended](https://stackoverflow.com/questions/26110828/should-i-use-dockerfiles-or-image-commits).
- Where should the data for the project be on the server?
  - The data folder of the host machine can be exposed to a container by passing `--volume path/from/host:/path/to/container` at `docker container run`. For now, we can store the data (corpora) under each of our own home directories.
- What is your coding environment with Docker?
  - You can directly code inside the container using Vim or Emacs.
  - You can use Jupyter or JupyterLab inside the container and expose corresponding ports.
  - You can set up a remote environment in [VSCode](https://code.visualstudio.com/docs/remote/containers).
  - You can probably do something similar with PyCharm as well.
- Can two users share the same image?
  - Yes. Two users can run two different containers of the same image. In the analogy of OOP, images are to classes as containers are to instances of classes.
- How do I decide what images I need?
  - You can either create images by writing Dockerfiles or pull existing images from [the Docker Hub](https://hub.docker.com/). You can check out the Dockerfile of the uploaded images.
  - You can also take a look at [zaemyung/dockerfiles](https://github.com/zaemyung/dockerfiles) for some ideas.
- How does GPU integration work?
  - Provided that you have an image with right CUDA and whatnots installed, `docker container run --gpus all` should expose all GPUs to the container.
- I want to use Jupyter Notebook!
  - TL;DR
    - Expose the notebook port when creating a container by specifying port flag: `-p 8888:8888`
    - Inside the container, install and launch `jupyter-lab` or `notebook` with `--port 8888 --ip 0.0.0.0`
    - Do ssh tunneling: `ssh -N -f -L localhost:8888:localhost:8888 your_username@server.address`
    - On your local machine, connect via `http://127.0.0.1:8888/lab?token=your_token`
  - (Or better yet, you can just use VSCode that does all this for you.)
  - For more details, take a look [here](https://towardsdatascience.com/how-to-run-jupyter-notebook-on-docker-7c9748ed209f).

## Troubleshooting
- load library failed: libnvidia-ml.so.1: cannot open shared object file
  - `sudo apt-get purge docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin docker-ce-rootless-extras`
  - `sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin`
