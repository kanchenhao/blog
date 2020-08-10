---
title: MindSpore Tutorial In Docker
published: true
---

This is a MindSpore tutorial in WSL2's docker.

### Install WSL2
First, install WSL2. We can refer to the installation tutorial in [Windows 10 official website](https://docs.microsoft.com/en-us/windows/wsl/install-win10). I select **Ubuntu 20.04** linux distribution.

### Install Docker

```shell
$ curl -fsSL https://get.docker.com -o get-docker.sh
$ sudo sh get-docker.sh
$ sudo service docker start
$ sudo systemctl enable docker
$ sudo usermod -aG docker $USER
```

### Install MindSpore

We select CPU version to install：

```shell
$ docker pull mindspore/mindspore-cpu:0.3.0-alpha
```

<!-- more -->

After installation, you can see the image we installed:

```shell
$ docker images
REPOSITORY                TAG                 IMAGE ID            CREATED             SIZE
mindspore/mindspore-cpu   0.3.0-alpha         ef443be923bc        3 months ago        1.05GB
```

Then create our own container based on this image we just installed:

```shell
$ docker run -it mindspore/mindspore-cpu:0.3.0-alpha /bin/bash
```

### Download MindSpore

Download MindSpore Lenet code:

```shell
$ git clone https://github.com/mindspore-ai/docs.git
```

Save this change so that there is no need to repeat the clone when starting the container later. Docker supports only submitting incremental modifications based on the original image to form a new image. Later, use this new image as a template to start the container, and the cloned files will exist in the container, so there is no need to clone repeatedly.

First, with ```docker ps -l``` to find the container ID of the cloned mindspore package. Then submit this container as a new image, which is named **kanchenhao/mindspore** here.

```shell
$ docker ps -l
CONTAINER ID        IMAGE                                 COMMAND             CREATED              STATUS                     PORTS               NAMES
25e14b1016ac        mindspore/mindspore-cpu:0.3.0-alpha   "/bin/bash"         About a minute ago   Exited (0) 5 seconds ago                       vibrant_goodall
$ docker commit 25e14b1016ac kanchenhao/mindspore
$ docker images
REPOSITORY                TAG                 IMAGE ID            CREATED             SIZE
kanchenhao/mindspore      latest              f0556d73f219        22 seconds ago      1.13GB
mindspore/mindspore-cpu   0.3.0-alpha         e9b3f15488e5        2 months ago        1.03GB
```

### Run Lenet

```shell
$ docker run -it kanchenhao/mindspore /bin/bash
$ cd /docs/tutorials/tutorial_code
$ python lenet.py
============== Starting Training ==============
epoch: 1 step: 1, loss is 2.3035789
epoch: 1 step: 2, loss is 2.3001177
epoch: 1 step: 3, loss is 2.2996633
epoch: 1 step: 4, loss is 2.3047967
...
epoch: 1 step: 1872, loss is 0.12087243
epoch: 1 step: 1873, loss is 0.074895434
epoch: 1 step: 1874, loss is 0.09245071
epoch: 1 step: 1875, loss is 0.07100312
============== Starting Testing ==============
============== Accuracy:{'Accuracy': 0.9629407051282052} ==============
```

I will continue to share my study notes about MindSpore in the follow-up, welcome everyone to give me suggestions and leave comments.