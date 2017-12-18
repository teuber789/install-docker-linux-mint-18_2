# install-docker-linux-mint-18_2
Instructions for how to install Docker CE on Linux Mint 18.2

### The problem
I attempted to install Docker CE on my Linux Mint 18.2 laptop following [these instructions provided by Docker](https://docs.docker.com/engine/installation/linux/docker-ce/ubuntu/#install-docker-ce). However, I kept getting the following error after running the ```sudo apt-get install docker-ce``` command: 

```
$ sudo apt-get install docker-ce
Reading package lists... Done
Building dependency tree       
Reading state information... Done
E: Unable to locate package docker-ce
```

### The reason
The reason this happens is because the ```$(lsb_release -cs)``` string evaluates to ```sonya``` in Linux Mint. Instead, we need it to evaulate to ```xenial```, which is the code name of the Ubuntu distribution that Linux Mint 18.2 is based on.

### The fix
The fix is to insert ```xenial``` instead of ```$(lsb_release -cs)```.

The modified setup instructions are:
```bash
$ sudo apt-get remove docker docker-engine docker.io
$ sudo apt-get update
$ sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    software-properties-common
$ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
# This line changed
$ sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu xenial stable"
$ sudo apt-get update
$ sudo apt-get install docker-ce
$ sudo docker run hello-world
```
