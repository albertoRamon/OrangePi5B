
_Default user/password orangepi/orangepi_

### Install Balenaetcher on Orange PI (ARM64)
[GitHub Releases](https://github.com/Itai-Nelken/BalenaEtcher-arm/releases/)
 ```bash
https://github.com/Itai-Nelken/BalenaEtcher-arm/releases/download/v1.7.9/balena-etcher-electron_1.7.9+5945ab1f_arm64.deb
sudo apt install -y --fix-broken ./balena-etcher-electron_1.7.9+5945ab1f_arm64.deb
```


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



# Graphics Acelerator (Joshua-Riek) (RKDevTool)
* [GitHub](https://github.com/Joshua-Riek/ubuntu-rockchip) 
   * [Wiki Project](https://github.com/Joshua-Riek/ubuntu-rockchip/wiki)
   * [Wiki Rock-5B](https://github.com/Joshua-Riek/ubuntu-rockchip/wiki/Rock-5B)
* Video: [NEW Orange Pi 5B. Installing Custom Ubuntu to eMMC drive](https://www.youtube.com/watch?v=5q_tytwmseg&t=756s)
* Is a custom Ubuntu (v22.04.2 LTS) for RK3588 CPU
  Josua added a PPA (Own repository [DEB Repository](https://launchpad.net/~jjriek/+archive/ubuntu/orangepi5)) 
     * Thus, _sudo apt update_ will solve some problems
	 * Include some custom tools
	 
![alt text](/Pictures/14.png)

1. Download IMG from [releases](https://github.com/Joshua-Riek/ubuntu-rockchip/releases) last version.
2. Download RKDevTool_Release[Download](https://drive.google.com/drive/folders/1bSaTxyTlwsEjBhanBly4-lqzzVVtOFSj).
3. Install DriverAssistant (is inside)
4. /RKDevTool_Release/
   * Configure English: Config (Configuration Settings): "Selected=2"
   
![alt text](/Pictures/12.png)
   
   
   * Open RKDevTool: You will see "No device"
   ![alt text](/Pictures/13.png)
5. Switch on Power **Presing** "MaskROM Key"
    ![alt text](/Pictures/15.png)
6. "Boot" > "Load Config": 
    ![alt text](/Pictures/16.png)
	
	MiniLoader > RK3588_linux_emmc
	![alt text](/Pictures/17.png)

	Replace Loader:
	![alt text](/Pictures/18.png)
	For this:
	![alt text](/Pictures/19.png)
	
	Check: "Write by adress" and "RUN"
	![alt text](/Pictures/20.png)


## Install TF & eMMC
[Wiki for Orange PI 5B](https://github.com/Joshua-Riek/ubuntu-rockchip/wiki/Orange-Pi-5B)
 1. Use Balena to copy the IMG from [releases](https://github.com/Joshua-Riek/ubuntu-rockchip/releases)
 2. Boot using the Memory Card
 3. Check if eMMC is detected
 
```bash
  lsblk /dev/mmcblk0
  NAME        MAJ:MIN RM   SIZE RO TYPE MOUNTPOINTS
  mmcblk0     179:0    0  58.2G  0 disk 
 ```
 
 4. Copy Ubuntu to eMMC
 ```bash
  xz -dc ubuntu-22.04.2-preinstalled-desktop-arm64-orangepi5b.img.xz | sudo dd of=/dev/mmcblk0 bs=4k
  sync
```

## Test what acelerations are enabled (Chromium)
(Pag 273)

1. Open Chromium
2. Go to: _chrome://gpu_
![alt text](/Pictures/10.png)

## Enable acelerations

## Benchmarks [Graphics / GPU] 
(Pag 271)

* Option 1
 ```bash
  glmark2              #Check if GL_Vendor Appear
```
* Option 2
 ```bash
  gpu_load.sh
```

* Option 3: (Pag 274)
 ```bash
  # 1- Open a video, like /usr/local/test.mp4
  # 2- Run Script
  vpu_debug.sh
```

## Install Docker
(Pag 186)
Is already installed but need be enabled

```bash
enable_docker.sh
docker run hello-world
```

## Install BT
(Pag 189)
* [www.BT.ch](https://www.bt.cn/new/index.html)
* Looks Very oriented to Chineese Market
```bash
sudo install_bt_panel.sh
```

## NoMachine
(Pag 212)
* [www.nomachine.com](https://www.nomachine.com/) [/getting-started](https://www.nomachine.com/getting-started-with-nomachine)
* Is Free but no GPL (Have an Enterprise version)


## VNC (Server Ubuntu v22.04) [RDP Server]
(Pag 217)
**Check the script, what version of VNC is installing**
```bash
sudo set_vnc.sh
# 1. Configure Password
# 2. The SRV is running you must be able to connect (IE. MobaxTerm, Windows RDP)
#    Default Port: 5901
```

* startup script: _/root/.vnc/xstartup_
* Log file: _/root/.vnc/orangepi5b:1.log_


## Other Languages (Ubunt v22.04, Jammy)

### GCC
(Pag 226)
Installed by default
```bash
gcc --version
```

### Python3
(Pag 223)
Installed Python3 by default
```bash
python3 --version
```

### Java
(Pag 223)
**????Check that is correct:**

Installed Java RE by default: (OpenJDK Runtime Environment v18)
```bash
java --version
```

Java JDK need be installed
```bash
sudo apt install -y openjdk-18-jdk
javac --version
```

##  Install kernel Headers
(Pag 245)

* Method 1: Download from [Official Tools](https://drive.google.com/drive/folders/1iBvN29Ls9iKrn91sJGUHmQzz89SLMASh)
```bash
sudo dpkg -i linux-headers-legacy-rockchip-rk3588_1.x.x_arm64.deb
```
* Method 2: Compiling the Kernel from Source Code (Pag 305)


## Activate Wayland
(Pag 267)

Ubuntu Settings> About > Windowing System
![alt text](/Pictures/10.png)


## Compile our "Orange-Build"
(Pag 297)