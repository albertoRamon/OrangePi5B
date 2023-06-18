
# Install Ubuntu 
If the image is Android is different !!

## Using Windows Balena on TF Card (Memory Card)
(Pag 21)
* [Download](https://drive.google.com/drive/folders/1xhP1KeW_hL5Ka4nDuwBa8N40U8BN0AC9) Image
   Current Version: 1.0.2
* Use [Balena](https://etcher.balena.io/#download-etcher) to burn the IMG file into TF Card **As Admin**
* Insert MMcard and start Orange PI

## Using Windows RKDevTool on TF Card (Memory Card)
(PAG 25)
* [Download](https://drive.google.com/drive/folders/1bSaTxyTlwsEjBhanBly4-lqzzVVtOFSj) DriverAssistant and MiniLoader
* [Download](https://drive.google.com/drive/folders/1xhP1KeW_hL5Ka4nDuwBa8N40U8BN0AC9) Image
* Connect you PC with Orange PI and MMcard into Orange PI
*  [RKDevTool]()

## Using Windows RKDevTool on eMMC
(PAG 40)
* [Download](https://drive.google.com/drive/folders/1bSaTxyTlwsEjBhanBly4-lqzzVVtOFSj) MiniLoader, RKDevTool_Release and DriverAssistant
* [Download](https://drive.google.com/drive/folders/1xhP1KeW_hL5Ka4nDuwBa8N40U8BN0AC9) Image
* DriverAssitant > DriverInstall.exe: Install Rockchip driver
* RKDevTool:
	* Check status USB
	* Connect **USB DATA** to PC with Orange PI and MMcard into Orange PI
	* Press (& hold) MaskROM Buttom
	* Connect **USB POWER**
	* Check status USB

# Debug
(Pag 81)
* Need a conversor TTL to USB at 1500000 bauds


# Graphics Acelerator (Joshua-Riek)
[GitHub](https://github.com/Joshua-Riek/ubuntu-rockchip) [Wiki](https://github.com/Joshua-Riek/ubuntu-rockchip/wiki) [releases](https://github.com/Joshua-Riek/ubuntu-rockchip/releases)

Is a custom Ubuntu (v22.04.2 LTS) for RK3588 CPU

## Install TF & eMMC
[Wiki for Orange PI 5B](https://github.com/Joshua-Riek/ubuntu-rockchip/wiki/Orange-Pi-5B)
 1. Use Balena to copy the IMG from [releases](https://github.com/Joshua-Riek/ubuntu-rockchip/releases)
 2. Boot using the Memory Card
 3. Check if eMMC is detected
 ```
lsblk /dev/mmcblk0
NAME        MAJ:MIN RM   SIZE RO TYPE MOUNTPOINTS
mmcblk0     179:0    0  58.2G  0 disk 
 ```
 4. Copy Ubuntu to eMMC
 ```
xz -dc ubuntu-22.04.2-preinstalled-desktop-arm64-orangepi5b.img.xz | sudo dd of=/dev/mmcblk0 bs=4k
sync
```

## Test what acelerations are enabled

## Enable acelerations

## Benchmarks [Graphics]