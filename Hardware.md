
# Orange Pi 5B: Hardware
 [Link](http://www.orangepi.org/html/hardWare/computerAndMicrocontrollers/details/Orange-Pi-5B.html)

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
![alt text](/Pictures/04.png)
* Red: Power indication (no controlable by soft)
* Green: Kenerl start ==> Blink (controled by soft)
```bash
sudo su
cd /sys/class/leds/status_led


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



### GPIO
![alt text](/Pictures/02.png)
