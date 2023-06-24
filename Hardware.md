
# Orange Pi 5B: Hardware
 
![alt text](/Pictures/00.png)
![alt text](/Pictures/01.png)

### CPU:
* Rockchip RK3588S
* 64 Bits ARM
* x4 Cores A76 2.4 GHz 
* x4 Cores A55 1.8 GHz 
* Is a simplied version of Rockchip RK3588. 
   [Comparative](https://gadgetversus.com/processor/rockchip-rk3588-vs-rockchip-rk3588s/): 4x 3PCIe vs 1x PCIe Lanes

### GPU:
* [Mali-G610 MP4](https://www.arm.com/products/silicon-ip-multimedia/gpu/mali-g610)

### RAM
* 4GB/8GB/16GB/32GB
* LPDDR4/4x

### HD:
* eMMC
* 32GB/64GB/128GB/256GB

### External connections
[See GPIO](https://github.com/albertoRamon/OrangePi5B/blob/main/Hardware.md#gpio)

* HDMI
* 1x USB3.0-C (**NO** Power IN) Video Display Port (DP) 1.4
* 2x USB2.0 (one is shared with USB-C)
* 2x USB3.0
* HDMI 2.1 8K 60KHz
* 26 PIN expansion
* Cammera
   * 1x MIPI CSI 4Lane
   * 2x MIPI D-PHY RX 4Lane
* Ethernet 1G (YT8531C )
* WI-FI6+BT 5.0 module (AP6275P), supports BLE
* RTC ??


### Leds
(Pag 100)
![alt text](/Pictures/04.png)
* Red: Power indication (no controlable by soft)
* Green: Kenerl start ==> Blink (controled by soft)
```bash
sudo su
cd /sys/class/leds/status_led
echo none > trigger			#Stop flash
echo default-on > trigger	#Always ON
echo heartbeat > trigger	#Blink

```

### Power  Supply
(Pag 89)

![alt text](/Pictures/03.png)
* Power  USB-C: connector format USB-C 5V/4A: **In the corner**
* Power  USB-C: doesn't support [Power Delivery (PD) negotiation](https://www.usb.org/usb-charger-pd)
  (To provide more Watts, some USB uses 28V, 36V, and 48V insteand 5V)
  
* Power Management Unit(PMU): RK806-1 [PDF](https://rockchip.fr/RK809%20datasheet%20V1.01.pdf)
   * Input: 2.7 -5.5V 
   * Provide Real Time Clocl (RTC)
   * 9 Channels DC-DC, that can be monitorized by I2C
  
* The Pin 26, always provide 5v (directly from USB)
   * No configuration needed & can't be enalbed / disabled
   * No PWM feature
   * Max ????
   * This PIN can be use to Power the Board too (but no recomended)

|  **Don't confuse with the USB-C for data: In the middle** |
| --- | 



# GPIO
(Pag 160) 

| CNT    | TYPE     | Link  |
| ---    |    ----  |   --- |
|  x16   |   GPIO   |  [Link]()  |
|  x6    |   PWM    |  [Link](https://github.com/albertoRamon/OrangePi5B/blob/main/Hardware.md#pwm) |
|  x2    |   CAN    |  [Link](https://github.com/albertoRamon/OrangePi5B/blob/main/Hardware.md#can) |
|  x4    |   UART   |  [Link](https://github.com/albertoRamon/OrangePi5B/blob/main/Hardware.md#i2c) |
|  x3    |   I2C    |  [Link](https://github.com/albertoRamon/OrangePi5B/blob/main/Hardware.md#uart) |
|  x1    |   SPI    |  [Link](https://github.com/albertoRamon/OrangePi5B/blob/main/Hardware.md#spi) |



![alt text](/Pictures/02.png)
![alt text](/Pictures/05.png)

![alt text](/Pictures/06.png)


* GPIOs work 3.3v
* PIN22 can ve configured as poweroff
  we need solder a 100K Resistor
  ![alt text](/Pictures/07.png)
  
### WiringOP (Bash)
(Pag 163)  AQUI !!
* Is included in the Linux Image. If you want upate
   * Option 1:[Download DEB File](orangepi-build/external/cache/debs/arm64)  << Falta link al GIT
   * Option 2: Download from GIT and compile
   
```bash
sudo apt update
sudo apt install -y git
it clone https://github.com/orangepi-xunlong/wiringOP.git -b next
cd wiringOP
sudo ./build clean
sudo ./build
```

* Use 
```bash
gpio readall
```
### WiringOP (Python)
(Pag 174)
Internally use WiringOP Bash
```bash

```


### orangepiEnv
(pag 164)
*  Configure the funcaionality of multifunction pin: /boot/orangepiEnv.txt
```bash
sudo vim /boot/orangepiEnv.txt
```

## PWM
(Pag 172)
* 6 PWM: PWM0, PWM1, PWM3, PWM13, PWM14, PWM15

|  PWM |  PIN   | Memory  |
| --- | --- |  --- | 
| PWM00 | 18 (M1) | fd8b0000 |
| PWM01 | 16 (M1) or 26 (M2)| fd8b0010 |
| PWM03 | 15 (M0) or 23 (M2) | fd8b0030 |
| PWM13 | 03 (M0)| febf0010 |
| PWM14 | 11 (M1)| febf0020 |
| PWM15 | 07 (M0)| febf0030 |

* What means "\_IR\_" in the name of the pin?? No Idea
* On Linux system PWM PIN26 is disabled by default using:
```bash
sudo vim /boot/orangepiEnv.txt
overlays=pwm0-m1 pwm13-m2 pwm14-m1 pwm15-m2   # RESTART Linux !!!
```
* Afer enalble PWM will appear more pwmchip<XX>
To know <XX> what PWM is related:
```bash
sys/class/pwm/ -l  #Check the memory
```

* Files pwmchip<XX>
   * export
   * period
   * duty_cyple
   * enable
* Configure pwmchip<XX> 50 Hz (NO Symetric)
```bash
sudo su
echo 0 > /sys/class/pwm/pwmchip2/export
echo 20000000 > /sys/class/pwm/pwmchip2/pwm0/period
echo 1000000 > /sys/class/pwm/pwmchip2/pwm0/duty_cycle
echo 1 > /sys/class/pwm/pwmchip2/pwm0/enable
```

## SPI
(Pag 179)


## I2C
(Pag 181)

## CAN

## UART