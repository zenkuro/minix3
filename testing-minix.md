# Testing Minix

This guide provide decription on running Minix on Lenaro hosted on Centos7.

[It is based on official wiki page](https://wiki.minix3.org/doku.php?id=developersguide:minixonlinaroqemuarm)

The folowing action is done after Minix compilation on the same platform(therefore it might require additional dependencies).

## Build Linaro Qemu

Linaro provides open source software for ARM SoCs.
Linaro Qemu is a custom version of Qemu that supports the BeagleBoard-xM.
Linaro Qemu currently only supports python 2.
If you have both python 2 and 3 installed, you may have to specify the path to python by adding the configure argument –python=/usr/bin/python2.

```bash
$ cd $HOME
$ git clone git://git.linaro.org/qemu/qemu-linaro.git linaro
$ cd linaro
$ sudo yum install gtk2-devel libfdt-dev libfdt ncurses-devel
$ ./configure --target-list=arm-softmmu --prefix=$HOME/qemu --disable-werror 
$ make
$ make install
```

Now you have a QEMU in $HOME/qemu/bin/qemu-system-arm and can test a BeagleBoard-xM build on qemu by running:

```bash
# $HOME/qemu/bin/qemu-system-arm  -M beaglexm -drive if=sd,cache=writeback,file=minix_arm_sd.img -clock unix -serial stdio -device usb-kbd -device usb-mouse -usb
```

If you run into problems booting Minix with Linaro Qemu current, try QEMU emulator version 1.3.0 (qemu-linaro 2012.12). It is known to work with Minix current.

For reference: this page used to advise checking out an older version of qemu-linaro. This is no longer necessary; in fact, building the older version now no longer works on modern system. The qemu-linaro commit we previously recommended checking out was 
--disable-werror --enable-mc 

