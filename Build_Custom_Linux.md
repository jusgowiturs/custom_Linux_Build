#  1. Official Linux Kernel (Recommended)
 The Linux Kernel Organization
Website: https://www.kernel.org
This is the canonical source


## Creating Busy Box for FileSystem
# prerequisite
```bash
sudo apt update
sudo apt install gcc-arm-linux-gnueabihf make build-essential flex bison libssl-dev libelf-dev  bc 
echo "Host GCC:"; gcc --version | head -n1
echo "Make:"; make --version | head -n1
echo "Flex:"; flex --version | head -n1
echo "Bison:"; bison --version | head -n1
echo "ARM Cross-Compiler:"; arm-linux-gnueabihf-gcc --version | head -n1

```



arm-linux-gnueabihf-gcc -o hello helloworld.c

# For Persistant  initramfs  workspace
```bash
mkdir -p ~/initramfs_base
sudo cp -r /tmp/initramfs/* ~/initramfs_base/
```


make ARCH=arm CROSS_COMPILE=arm-linux-gnueabihf- -j$(nproc)