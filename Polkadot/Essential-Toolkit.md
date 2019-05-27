<div style="text-align: justify">

# Delegators Essential Toolkit Guide


## Command Line Only


### Introduction

This tutorial showcases installation of essential tools required for the interaction with [Polkadot Network](https://polkadot.network). If you choose to follow this tutorial make sure you run a clean machine with freshly installed Ubuntu 18.04 LTS operating system installed or follow or complete our **[Create Secure Environment Guide](TBD)**. Another (but NOT recommended) option is to run a virtual machine using virtualization software such free [VirtualBox](https://www.virtualbox.org/) and installing Ubuntu as VM to add another security layer but it will not protect you against malware that is potentially already hosted on machine such as keyloggers.

_NOTE: If you choose to not follow **[Creating Secure Environment Guide](TBD)** and continue with your everyday "use" operating system we can't guarantee safety of your assets and some of the commands might cause breaking changes to your operating system. Remember that Antivirus / Antimalware software will never protect you against all threats and exploits that can reside on your everyday use Laptop or Personal Computer._


### Prerequisites

*   Completing [Creation of Secure Environment Guide](TBD) or clean installation of Ubuntu 18.04


### Steps To Complete

*   Installing Rust and Essential Developer tools


## Setup using Ubuntu 18.04 LTS


### Installing Essential Toolkit

#### Installing Build Tools

Login to your account and enter terminal console by key combination of: **CTRL+ALT+T**

Install and upgrade essential build tools, by typing or copy pasting following commands into Terminal console and confirming them with **ENTER** key:


```
sudo -s

# enable yarn repository
curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add -
echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list

apt-get -y update && apt-get -y upgrade && apt-get -y install build-essential zip unzip jq git make clang cmake pkg-config libssl-dev yarn npm

# install latest node
npm install -g n
n stable
```


#### Installing Rust

```
cd /home/ubuntu
# note: do not use root account to execute following command, type exit command to logout is you are sudo '#'
curl https://sh.rustup.rs -sSf | sh

sudo -s
nano /etc/profile
```


Using arrow keys navigate to the bottom of the file and append following line:


```
export PATH=$PATH:$HOME/.cargo/bin
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
source $HOME/.cargo/env
```


To save changes press combination of keys: **CTRL+O**, **[ENTER]**, **CTRL+X**

To update rust and verify version run following two commands (without having to restart your machine)


```
source /etc/profile
source $HOME/.cargo/env

rustup update

rustup -V && cargo -V && -rustc -V
```

Console should response with 3 version messages and you can proceed to install `polkadot`.



#### Installing polkadot

```
cd /home/ubuntu
git clone https://github.com/paritytech/polkadot.git
cd polkadot
cargo clean
git checkout v0.4
git pull origin v0.4
./scripts/init.sh
./scripts/build.sh
cargo install --path ./ --force
```

</div>
