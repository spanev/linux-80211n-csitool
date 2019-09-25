# Linux 802.11n CSI Tool for newer Linux kernels

## Intro
The purpose of this repository is to provide support for building the CSI-enabled Wi-Fi drivers for **Intel Wireless Link 5300** adapters on Linux distributions with newer kernel versions. At this point this code has been tested on **Ubuntu 16.04** and **Ubuntu 18.04** with kernel version **4.15**. More tests are expected soon.

The code presented here comprises of a modified version of the Linux kernel. The modifications were made by examining the code provided by [dhalperi/linux-80211n-csitool](https://github.com/dhalperi/linux-80211n-csitool/) and adapting them to more recent Linux kernel versions - **iwlwifi** module. The building and installation instructions were taken from the original [Linux 802.11n CSI Tool](http://dhalperi.github.io/linux-80211n-csitool/) website and adapted accordingly.

## Installation Instructions

### Prerequisites

#### Kernel version

Before proceeding further, you need to check the version of your kernel. It should be 4.15. The following command will print that information:

```shell
$ uname -r
```

#### Compilers with retpoline support

Newer kernels require compilers with retpoline supports.  GCC and G++ version 7.3 and above support that feature. The example below shows how to install GCC/G++ version 8:

```shell
$ sudo add-apt-repository ppa:ubuntu-toolchain-r/test
$ sudo apt update
$ sudo apt install gcc-8 g++-8
```

If you install different version of the compilers, you need to modify the Makefile.

Additional packages which are required, but you may not have

```shell
$ sudo apt install make linux-headers-$(uname -r) git-core
```

TODO: Put 2 tips

### Build and Install the Modified Wireless Driver

ToDo


### Install the Modified Firmware

ToDo


### Build the Userspace Logging Tool

ToDo


### Enable Logging and Test

ToDo

