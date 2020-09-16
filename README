```
$sudo apt install git bc bison flex libssl-dev make
$git clone --depth=1 --branch rpi-5.4.y git@github.com:DynamicDeepSKY/linux.git
$cd linux
$make menuconfig (save w/o any change)
$KERNEL=kernel7l
$make bcm2711_defconfig
$vim .config
CONFIG_LOCALVERSION="-v7l-DDS-KERNEL-FBTFT"
$make -j4 zImage modules dtbs
$sudo make modules_install
$sudo cp arch/arm/boot/dts/overlays/*.dtb* /boot/overlays/
$sudo cp arch/arm/boot/dts/overlays/README /boot/overlays/
$sudo cp arch/arm/boot/zImage /boot/$KERNEL.img
```


Linux kernel
============

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
