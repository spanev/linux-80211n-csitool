# Linux 802.11n CSI Tool for newer Linux kernels

## Intro
The purpose of this repository is to provide support for building the CSI-enabled Wi-Fi drivers for **Intel Wireless Link 5300** adapters on Linux distributions with newer kernel versions. At this point this code has been tested on **Ubuntu 16.04** and **Ubuntu 18.04** with kernel version **4.15**. More tests are expected soon.

The code presented here comprises of a modified version of the Linux kernel. The modifications were made by examining the code provided by [dhalperi/linux-80211n-csitool](https://github.com/dhalperi/linux-80211n-csitool/) and adapting them to more recent Linux kernel versions - **iwlwifi** module. The building and installation instructions were taken from the original [Linux 802.11n CSI Tool](http://dhalperi.github.io/linux-80211n-csitool/) website and adapted accordingly.

## Installation Instructions

### Prerequisites

#### Kernel version

Before proceeding further, you need to check the version of your kernel. It should be **4.15**, otherwise the commands below won't work. The following command will print that information:

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

You need to ensure that the <code>make</code> command uses the right version of the compilers. You can use either of these two ways do it

##### Modify the Makefile (local solution)
TODO

##### Redirect the system-wide links to the compiler executables (system-wide solution)
Check where the current links point to. The command
```shell
$ ls -l /usr/bin/gcc /usr/bin/g++
```
should generate an output similar to

```shell
lrwxrwxrwx 1 root 5 Mar 27  2018 /usr/bin/g++ -> g++-5
lrwxrwxrwx 1 root 5 Mar 27  2018 /usr/bin/gcc -> gcc-5
```
The current links are pointing to version 5. So they need to be redirected to version 8. To do that, remove the current links
```shell
$ sudo rm /usr/bin/gcc
$ sudo rm /usr/bin/g++
```
and create the new ones
```shell
$ sudo ln -s /usr/bin/gcc-8 /usr/bin/gcc
$ sudo ln -s /usr/bin/g++-8 /usr/bin/g++
```



#### Additional packages which are required, but you may not have installed on your system

```shell
$ sudo apt install make linux-headers-$(uname -r) git-core
```

TODO: Put 2 tips

### Build and Install the Modified Wireless Driver

Clone the modified Linux kernel code
```shell
$ git clone https://github.com/spanev/linux-80211n-csitool.git
$ cd linux-80211n-csitool
```

Checkout the correct release version
(ToDo)

Build the modified driver for the existing kernel
```shell
$ make -C /lib/modules/$(uname -r)/build M=$(pwd)/drivers/net/wireless/intel/iwlwifi modules
```

```shell
$ sudo make -C /lib/modules/$(uname -r)/build M=$(pwd)/drivers/net/wireless/iwlwifi INSTALL_MOD_DIR=updates \
    modules_install
$ sudo depmod
$ cd ..
```
TODO: Tip

### Install the Modified Firmware

Obtain the CSI Tool supplementary material:
```shell
$ git clone https://github.com/dhalperi/linux-80211n-csitool-supplementary.git
```

Relocate any existing firmware for Intel Wi-Fi Link 5000 Series adapters:
```shell
$ for file in /lib/firmware/iwlwifi-5000-*.ucode; do sudo mv $file $file.orig; done
```

Install the modified firmware:
```shell
$ sudo cp linux-80211n-csitool-supplementary/firmware/iwlwifi-5000-2.ucode.sigcomm2010 /lib/firmware/
$ sudo ln -s iwlwifi-5000-2.ucode.sigcomm2010 /lib/firmware/iwlwifi-5000-2.ucode
```

### Build the Userspace Logging Tool

ToDo


### Enable Logging and Test

ToDo

