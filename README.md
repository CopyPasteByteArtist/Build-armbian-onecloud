
# 2026-07 Update
  这个仓库的Onecloud (WS1608) 刷机包不再更新

## 我维护的另一个跟随Armbian官方镜像更新的Amlogic USB Burning Tool线刷包项目
  
  短接线刷后Armbian系统工作稳定，目前有下面官方img打包的线刷包，并且还在更新
  
   ```
  Armbian_23.11.1_Onecloud_jammy_current_6.1.63_minimal.img.xz
  Armbian_23.11.1_Onecloud_bookworm_current_6.1.63_minimal.img.xz
  Armbian_24.8.1_Onecloud_noble_current_6.6.43_minimal.img.xz
  Armbian_24.8.1_Onecloud_bookworm_current_6.6.43_minimal.img.xz
  Armbian_24.11.1_Onecloud_noble_current_6.6.43_minimal.img.xz
  Armbian_24.11.1_Onecloud_bookworm_current_6.6.43_minimal.img.xz
  Armbian_community_26.2.0-trunk.904_Onecloud *
  Armbian_community_26.8.0-trunk.121_Onecloud *
  Armbian_community_26.8.0-trunk.170_Onecloud *
  Armbian_community_26.8.0-trunk.359_Onecloud *
  Armbian_community_26.8.0-trunk.413_Onecloud *
  ...
  ```
  你可以用官方的其它 Armbian *.img.xz USB/SD卡镜像包打包成 USB Burning Tool 线刷包，实现DIY
  
  仓库地址
  [armbian-official-onecloud-usb-burn-images](https://github.com/CopyPasteArtisan/armbian-official-onecloud-usb-burn-images)

  
  Actions工作流程参考了 https://github.com/hzyitc/armbian-onecloud 项目，感谢@hzyitc

### 如果AMD平台笔记本/台式机用Amlogic USB Burning Tool刷入镜像时报错，换Intel平台的笔记本/台式机再刷机，这是USB兼容性问题。我没试过用USB转接器/拓展坞能不能解决这个问题。




# 以下是存档
## Armbian for Onecloud
  Armbian for Onecloud(WS1608)，Amlogic S805 CPU (32bit)，1G RAM + 8G eMMC ROM，1GbE，AKA 玩客云3、赚钱宝3

### First-time login

  Hostname: `onecloud`
  
  Username: `root`
  
  Password: `1234`

### Boot from `u-boot` 

#### Boot from `USB`

  ```
  setenv bootdev "usb 0"
  usb start
  fatload ${bootdev} 0x20800000 boot.scr && autoscr 0x20800000
  ```

#### Boot from `eMMC`

  ```
  setenv bootdev "mmc 1"
  fatload ${bootdev} 0x20800000 boot.scr && autoscr 0x20800000
  ```

### GPIO

  There is a reserved SDIO WiFi module on the board which has many pins directly connected to the `SoC`. They are able to be used as `GPIO`.
  
  Please check the `dts` (added by `patch/kernel/archive/meson-6.12/onecloud-0001-add-dts.patch`) for specific definitions.
  
  NOTE: These pins in the `dts` were measured on `V1.0 board` and have not been verified on the V1.3 board.

### Related link

  [`armbian/build`](https://github.com/armbian/build) - Armbian official repository
  
  [`xdarklight/linux@meson-mx-integration-5.18-20220417`](https://github.com/xdarklight/linux/tree/meson-mx-integration-5.18-20220417) - the source code of `HDMI` patch
  
  [`S805_Datasheet V0.8 20150126.pdf`](https://dn.odroid.com/S805/Datasheet/S805_Datasheet%20V0.8%2020150126.pdf) - S805 datasheet
