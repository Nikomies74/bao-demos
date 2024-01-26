# Nvidia Tegra TX2

---

**NOTE**

<!--- instruction#1 -->
## 1) Flash the firmware

Set your board to recovery mode by:

1) Power it off completely. If needed unplug and replug the power cord.
2) Press down the Recovery button. While pressing the Recovery button, press
the Power button. Wait for the board to turn on.
3) Connect to the board using USB through the J28 micro-USB port.
4) Flash the board:

```
# what is
cd $BAO_DEMOS_NVIDIA_TOOLS/Linux_for_Tegra
sudo ./flash.sh -k secure-os --image $BAO_DEMOS_WRKDIR_PLAT/tos.img\
    --bup jetson-orin-nano-devkit mmcblk0p1
```

sudo ./flash.sh -k secure-os --image /home/haataine/tii/bao/bao-demos/wrkdir/imgs/nx16tos.img --bup jetson-orin-nano-devkit mmcblk0p1

If all goes well you should see the message:

```
*** The [secure-os] has been updated successfully. ***
```

<!--- instruction#2 -->
## 2) Setup SD card

After [preparing your sd card](../../platforms/sdcard.md), copy bao's final
image to it:

```
cp $BAO_DEMOS_WRKDIR_IMGS/bao.bin $BAO_DEMOS_SDCARD
umount $BAO_DEMOS_SDCARD
```

<!--- instruction#3 -->
## 3) Setup board

Insert the sd card in the board's sd slot.

Connect to the TX2's UART using a USB-to-TTL adapter. Use a terminal
application such as `screen`. For example:

```
screen /dev/ttyUSB0 115200
```

Turn on/reset your board.

<!--- instruction#4 -->
## 4) Run u-boot commands

You will get u-boot's prompt. Load the bao image, and jump to it:

```
fatload mmc 1 0xa0000000 bao.bin; go 0xa0000000
```

You should see the firmware, bao and its guests printing on the UART.

At this point, depending on your demo, you might be able connect to one of the
guests via ssh by connecting to the board's ethernet RJ45 socket.

<!--- instruction#end -->

<!-- Links -->

[tegra-bsp]: https://developer.nvidia.com/embedded/linux-tegra
