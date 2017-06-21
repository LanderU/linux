## Kernel for Raspberry Pi

### Cross-compiling the kernel on Linux

Download Raspberry Pi tools:
```
git clone https://github.com/raspberrypi/tools.git
```

Export the following variables to specify cross-compilation options:
```
export ARCH=arm 
export CROSS_COMPILE=~/tools/arm-bcm2708/gcc-linaro-arm-linux-gnueabihf-raspbian/bin/arm-linux-gnueabihf-
```

If you compile on a x64-machine you need to change the last export to: 
```
export CROSS_COMPILE=~/tools/arm-bcm2708/gcc-linaro-arm-linux-gnueabihf-raspbian-x64/bin/arm-linux-gnueabihf-
```

For Raspberry Pi1/Zero:
```
make bcmrpi_defconfig
```

For Raspberry Pi 2/3:
```
make bcm2709_defconfig
```

Optional: make changes to the config
```
make menuconfig
```

Compile the kernel:
```
make -j5
```

Install modules, will result in "lib" folder with modules and firmware:
```
mkdir mods
INSTALL_MOD_PATH=mods make modules_install
```

### Setting up an SD card with the compiled kernel

Copy kernel:

For Raspberry Pi:
```
Copy arch/arm/boot/Image to /boot/kernel.img on SD card.
Copy arch/arm/boot/dts/bcm2708-rpi-b.dtb to /boot/bcm2708-rpi-b.dtb on SD card
Copy arch/arm/boot/dts/bcm2708-rpi-b-plus.dtb to /boot/bcm2708-rpi-b-plus.dtb on SD card
Copy (merge if necessary) mods/lib to / on SD card.
```

For Raspberry Pi 2:
```
Copy arch/arm/boot/Image to /boot/kernel7.img on SD card.
Copy arch/arm/boot/dts/bcm2709-rpi-2-b.dtb to /boot/bcm2709-rpi-2-b.dtb on SD card
Copy (merge if necessary) mods/lib to / on SD card.
```

For Raspberry Pi 3:

```
Copy arch/arm/boot/Image to /boot/kernel7.img on SD card.
Copy arch/arm/boot/dts/bcm2710-rpi-3-b.dtb to /boot/bcm2710-rpi-3-b.dtb on SD card
Copy arch/arm/boot/dts/bcm2710-rpi-cm3.dtb to /boot/bcm2710-rpi-cm3.dtb on SD card
Copy (merge if necessary) mods/lib to / on SD card.
```
