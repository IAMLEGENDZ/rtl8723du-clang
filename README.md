===========
rtl8723du
===========

This source code was modified to be compatible compiling with clang for kernels compiled with it.
=======
This repository includes drivers for the following card:

Realtek RTL8723DU

Tested with Linux Kernel versions (6.8 to 6.15) and it's working.

### Installation instruction
##### Requirements
You will need to install "make", "clang", "kernel headers", "kernel build essentials", and "git".

For **Ubuntu**: You can install them with the following command
```bash
sudo apt-get update
sudo apt-get install make clang linux-headers-$(uname -r) build-essential git
```
For **Fedora**: You can install them with the following command
```bash
sudo dnf install kernel-headers kernel-devel
sudo dnf group install "C Development Tools and Libraries"
```
For **openSUSE**: Install necessary headers with
```bash
sudo zypper install make clang kernel-devel kernel-default-devel git libopenssl-devel
```
For **OpenMandriva**: You can install them with the following command
```bash
sudo dnf install kernel-headers kernel-desktop-devel cmake glibc-devel lib64cppdap lib64crypt-devel lib64elfutils-devel lib64lzma-devel lib64ncurses-devel lib64rhash0 lib64z-devel lib64zstd-devel libc6 make
```
If any of the packages above are not found check if your distro installs them like that.

##### Installation
For all distros:
```bash
git clone git://github.com/IAMLEGENDZ/rtl8723du-clang.git
cd rtl8723du-clang
make CC=clang LD=ld.lld
sudo make install
```

##### How to unload/reload a Kernel module
 ```bash
sudo modprobe -rv 8723du         #This unloads the module
sudo modprobe -v 8723du          #This loads the module
```

***********************************************************************************************

When your kernel changes, then you need to do the following:
```bash
cd ~/rtl8723du-clang
git pull
make clean
make CC=clang LD=ld.lld
sudo make install
```

Remember, this MUST be done whenever you get a new kernel - no exceptions.

##### Installation with module signing for SecureBoot
For all distros:
```bash
git clone git://github.com/IAMLEGENDZ/rtl8723du-clang.git
cd rtl8723du-clang
make CC=clang LD=ld.lld
sudo make sign-install
```
You will be promted a password, please keep it in mind and use it in next steps.
Reboot to activate the new installed module.
In the MOK managerment screen:
1. Select "Enroll key" and enroll the key created by above sign-install step
2. When promted, enter the password you entered when create sign key. 
3. If you enter wrong password, your computer won't not bebootable. In this case,
   use the BOOT menu from your BIOS, to boot into your OS then do below steps:
```bash
sudo mokutil --reset
```
Restart your computer
Use BOOT menu from BIOS to boot into your OS
In the MOK managerment screen, select reset MOK list
Reboot then retry from the step make sign-install


