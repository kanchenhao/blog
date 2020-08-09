---
title: MindSpore Tutorial In Docker
published: true
---

This is a MindSpore tutorial in WSL2's docker.

### Install WSL2
First, install WSL2. We can refer to the installation tutorial in [Windows 10 official website](https://docs.microsoft.com/en-us/windows/wsl/install-win10). I select **Ubuntu 20.04** linux distribution.

### Install Docker：

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
$ docker pull mindspore/mindspore-cpu:0.1.0-alpha
```

<!-- more -->

After installation, you can see the image we installed:

```shell
$ docker images
REPOSITORY                TAG                 IMAGE ID            CREATED             SIZE
mindspore/mindspore-cpu   0.1.0-alpha         ef443be923bc        3 months ago        1.05GB
```

Then create our own container based on this image we just installed:

```shell
$ docker run -it mindspore/mindspore-cpu:0.1.0-alpha /bin/bash
```

Download MindSpore Lenet code and run it:

```shell
$ git clone https://github.com/mindspore-ai/docs.git
$ cd /docs/tutorials/tutorial_code
$ python lenet.py
============== Starting Training ==============
epoch: 1 step: 1, loss is 2.3024695
epoch: 1 step: 2, loss is 2.3015854
epoch: 1 step: 3, loss is 2.3041863
epoch: 1 step: 4, loss is 2.3041685
...
epoch: 1 step: 1872, loss is 0.24802093
epoch: 1 step: 1873, loss is 0.10461495
epoch: 1 step: 1874, loss is 0.28196782
epoch: 1 step: 1875, loss is 0.18189847
============== Starting Testing ==============
============== Accuracy:{'Accuracy': 0.9624399038461539} ==============
```


I will continue to share my study notes about MindSpore in the follow-up, welcome everyone to give me suggestions and leave comments.