# Armbian for Onecloud
Armbian for Onecloud(WS1608)，Amlogic S805 CPU (32bit)，1G RAM + 8G eMMC ROM，1GbE，AKA 玩客云3、赚钱宝3

## First-time login

Hostname: `onecloud`

Username: `root`

Password: `1234`

## Boot from `u-boot` 

### Boot from `USB`

```
setenv bootdev "usb 0"
usb start
fatload ${bootdev} 0x20800000 boot.scr && autoscr 0x20800000
```

### Boot from `eMMC`

```
setenv bootdev "mmc 1"
fatload ${bootdev} 0x20800000 boot.scr && autoscr 0x20800000
```

## GPIO

There is a reserved SDIO WiFi module on the board which has many pins directly connected to the `SoC`. They are able to be used as `GPIO`.

Please check the `dts` (added by `patch/kernel/archive/meson-6.12/onecloud-0001-add-dts.patch`) for specific definitions.

NOTE: These pins in the `dts` were measured on `V1.0 board` and have not been verified on the V1.3 board.

## Related link

[`armbian/build`](https://github.com/armbian/build) - Armbian official repository

[`xdarklight/linux@meson-mx-integration-5.18-20220417`](https://github.com/xdarklight/linux/tree/meson-mx-integration-5.18-20220417) - the source code of `HDMI` patch

[`S805_Datasheet V0.8 20150126.pdf`](https://dn.odroid.com/S805/Datasheet/S805_Datasheet%20V0.8%2020150126.pdf) - S805 datasheet
