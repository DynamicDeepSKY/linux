### Dependencies install, obtain kernel source, and setup
```
$sudo apt install git bc bison flex libssl-dev make
$git clone --depth=1 --branch dev/rpi-5.4.y-fbtft-dds git@github.com:DynamicDeepSKY/linux.git
$cd linux
$KERNEL=kernel7l
$make bcm2711_defconfig
$vim .config
```
change CONFIG_LOCALVERSION as some unique value (e.g.,)

`CONFIG_LOCALVERSION="-v7l-DDS-KERNEL-FBTFT"`

Kernel build (this will take 30 mins-1 hour depending on which modules set to build.)

```
$make -j4 zImage modules dtbs
```
Install built modules, device trees, and kernel image.
```
$sudo make modules_install
$sudo cp arch/arm/boot/dts/overlays/*.dtb* /boot/overlays/
$sudo cp arch/arm/boot/dts/overlays/README /boot/overlays/
$sudo cp arch/arm/boot/zImage /boot/$KERNEL.img
$sudo reboot
```
After bootup, type `uname -r` should show `v7l-DDS-KERNEL-FBTFT` string in the kernel version.

In order to use Adafruit-green LCD, add the following in `/boot/config.txt`
```
# Adafruit-green LCD support
 dtoverlay=adafruit18,green
```
reboot and type `lsmod`.
You can check `fb_st7735r` and `fbtft` were properly loaded.


```
Module                  Size  Used by
cmac                   16384  1
rfcomm                 45056  4
bnep                   20480  2
hci_uart               40960  1
btbcm                  16384  1 hci_uart
bluetooth             368640  29 hci_uart,bnep,btbcm,rfcomm
ecdh_generic           16384  2 bluetooth
ecc                    36864  1 ecdh_generic
fuse                  114688  3
8021q                  32768  0
garp                   16384  1 8021q
stp                    16384  1 garp
llc                    16384  2 garp,stp
fb_st7735r             16384  0
spidev                 20480  0
fbtft                  36864  1 fb_st7735r
...
```

# Linux kernel
---
There are several guides for kernel developers and users. These guides can
be rendered in a number of formats, like HTML and PDF. Please read
Documentation/admin-guide/README.rst first.

In order to build the documentation, use ``make htmldocs`` or
``make pdfdocs``.  The formatted documentation can also be read online at:

    https://www.kernel.org/doc/html/latest/

There are various text files in the Documentation/ subdirectory,
several of them using the Restructured Text markup notation.

Please read the Documentation/process/changes.rst file, as it contains the
requirements for building and running the kernel, and information about
the problems which may result by upgrading your kernel.
