<div style="text-align: justify">

# Delegators Essential Toolkit Guide


## Command Line Only


### Introduction

This tutorial showcases installation of essential tools required for the delegator to interact with [Cosmos Network](https://cosmos.network/intro). If you choose to follow this tutorial make sure you run a clean machine with freshly installed Ubuntu 18.04 LTS operating system installed or follow or complete our **[Create Secure Environment Guide](/Secure-Environment.md#creating-secure-environment)**. Another (but NOT recommended) option is to run a virtual machine using virtualization software such free [VirtualBox](https://www.virtualbox.org/) and installing Ubuntu as VM to add another security layer but it will not protect you against malware that is potentially already hosted on machine such as keyloggers when you will be retyping your fundraiser seed.

_NOTE: If you choose to not follow **[Creating Secure Environment Guide](/Secure-Environment.md#creating-secure-environment)** and continue with your everyday "use" operating system we can't guarantee safety of your coins and some of the commands might cause breaking changes to your operating system. Remember that Antivirus / Antimalware software will never protect you against all threats and exploits that can reside on your everyday use Laptop or Personal Computer._


### Prerequisites



*   Completing [Creation of Secure Environment Guide](/Secure-Environment.md#creating-secure-environment) or clean installation of Ubuntu 18.04


### Steps To Complete



*   Installing official fundraiser CLI tool


## Delegator Setup using Ubuntu 18.04 LTS


### Installing Essential Toolkit

#### Installing Build Tools

Login to your account and enter terminal console by key combination of: **CTRL+ALT+T**

Install and upgrade essential build tools, by typing or copy pasting following commands into Terminal console and confirming them with **ENTER** key:


```
sudo -s

apt-get -y update && apt-get -y upgrade && apt-get -y  install build-essential zip unzip jq git
```


#### Installing GOLANG

```

cd /tmp && wget https://dl.google.com/go/go1.11.5.linux-amd64.tar.gz && tar -xvf go1.11.5.linux-amd64.tar.gz && rm -r -v -f /usr/local/go && mv go /usr/local

mkdir -p $HOME/go/bin

nano /etc/profile
```


Using arrow keys navigate to the bottom of the file and append following 4 lines:


```
export GOROOT=/usr/local/go
export GOPATH=$HOME/go
export GOBIN=$GOPATH/bin
export PATH=$PATH:$GOROOT/bin:$GOPATH/bin:$GOBIN
```


To save changes press combination of keys: **CTRL+O**, **[ENTER]**, **CTRL+X**

(make sure above commands have no quotes or any other undesired characters copied by mistake)

In order to ensure .profile file is sourced open .bashrc file and source its content


```
nano $HOME/.bashrc
```


Using arrow keys navigate to the bottom of the file and append following 1 line:


```
source /etc/profile
```


To save changes press combination of keys: **CTRL+O**, **[ENTER]**, **CTRL+X**

To verify go version run following two commands (without having to restart your machine)


```
source /etc/profile

go version
```

Console should response with `go version go1.11.5 linux/amd64` message and you can proceed to install `cosmos-sdk`.


#### Installing cosmos-sdk


```
mkdir -p $GOPATH/src/github.com/cosmos && cd $GOPATH/src/github.com/cosmos && rm -rfv  ./cosmos-sdk

git clone https://github.com/cosmos/cosmos-sdk

cd cosmos-sdk && git checkout master

make tools install
```

</div>
