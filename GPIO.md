
# GPIO
(Pag 160) 

| CNT    | TYPE         | Link  |
| ---    |  ----        |   --- |
|  x16   |   GPIO       |       |
|  x6    |   PWM        |  [Link](https://github.com/albertoRamon/OrangePi5B/blob/main/Hardware.md#pwm) |
|  x2    |   CAN        |  [Link](https://github.com/albertoRamon/OrangePi5B/blob/main/Hardware.md#can) |
|  x4    |   UART       |  [Link](https://github.com/albertoRamon/OrangePi5B/blob/main/Hardware.md#i2c) |
|  x3    |   I2C        |  [Link](https://github.com/albertoRamon/OrangePi5B/blob/main/Hardware.md#uart)|
|  x1    |   SPI        |  [Link](https://github.com/albertoRamon/OrangePi5B/blob/main/Hardware.md#spi) |
|  x2    |   MIPI LCD   |  [Link](https://github.com/albertoRamon/OrangePi5B/blob/main/Hardware.md#mipi-lcd) |



![alt text](/Pictures/02.png)
![alt text](/Pictures/05.png)

![alt text](/Pictures/06.png)


| GPIOs work **3.3v** |
| ------------------- | 

| On Linux system PWM PIN26 is disabled by default using [orangepiEnv](https://github.com/albertoRamon/OrangePi5B/blob/main/Hardware.md#orangepienv) |
| ------------------------------------------------------------------- | 
* PIN22 can ve configured as poweroff
  we need solder a 100K Resistor
  ![alt text](/Pictures/07.png)
  
* Blink all GPIO:
```bash
sudo blink_all_gpio
```

### WiringOP: Use (Bash Version)
* Set using GPIO 
```bash
# Set PIN 7 (wPi 2): OUT Low Level
gpio mode 2 out     # Configure as "out"
gpio write 2 0      # Configure Low Level
gpio write 2 1      # Configure High Leve

```

* From Original PI version
   * [wiringpi.com](http://wiringpi.com/)
   * Manual [GPIO utility](https://projects.drogon.net/raspberry-pi/wiringpi/the-gpio-utility/)

```bash
gpio -v     #Print version
gpio more   <WiringPi Number> {in|outpwm|up|down|tri}
gpio write  <WiringPi Number> {0|1}
gpio pwm    <WiringPi Number> <value>  #0-1023
gpio read   <WiringPi Number>
gpio readall
```

Module Load Commands
```bash
gpio load spi [buffer size in KB]       #Default 4Kb
gpio load i2c [baud rate in Kb/sec]     #Default 100Kb/sec
```


??? Test IT:
```bash
gpio exports
```

### WiringOP: Install Bash Version
(Pag 163)
Wiring Orange Pi (OP) is a modification of WiringPI ( for Raspberry PI)

| Use **NEXT** Branch for Orange PI 5B |
| -- | 

* Is included in the Linux Image. If you want upate

   * Option 1: [Download DEB FileL orangepi-build/external/cache/debs/arm64/wiringpi_x.xx.deb](https://github.com/orangepi-xunlong/orangepi-build/tree/next/external/cache/debs/arm64)  from [OrangePi-Build](https://github.com/orangepi-xunlong/orangepi-build)
   * Option 2: Download from OrangePI Download page "[WiringOP Source Code compressed Package](https://drive.google.com/drive/folders/1gvCbQTMHh80S8H2MIha20nsXOoHVY3X3)"
   * Option 3: Download from [GIT](https://github.com/orangepi-xunlong/wiringOP/tree/next) and compile
   
```bash
sudo apt update
sudo apt install -y git
it clone https://github.com/orangepi-xunlong/wiringOP.git -b next
cd wiringOP
sudo ./build clean
sudo ./build
```

### WiringOP: Python Version
(Pag 174)
Internally use WiringOP Bash

* Install
```bash
sudo apt-get -y install git swig python3-dev python3-setuptools
git clone --recursive https://github.com/orangepi-xunlong/wiringOP-Python -b next
cd wiringOP-Python
python3 generate-bindings.py > bindings.i
sudo python3 setup.py install
python3 -c "import wiringpi; help(wiringpi)"	#Test that is installed
```

*  Example of Use (Pag 178)
```python
import wiringpi;
from wiringpi import GPIO; 
wiringpi.wiringPiSetup();
wiringpi.pinMode(2, GPIO.OUTPUT);
wiringpi.digitalWrite(2, GPIO.LOW
wiringpi.digitalWrite(2, GPIO.HIGH)
```
* Example Script
```bash
cd ~/wiringOP-Python/examples
python3 blink.py
```

### orangepiEnv
(Pag 164)
* The same can be done with 
*  Configure the funcaionality of multifunction pin: /boot/orangepiEnv.txt
```bash
sudo vim /boot/orangepiEnv.txt
overlays=pwm0-m1 pwm13-m2 pwm14-m1 pwm15-m2   # RESTART Linux !!!
overlays=spi4-m0-cs1-spidev                   # RESTART Linux !!!
overlays=i2c1-m2 i2c3-m0 i2c5-m3              # RESTART Linux !!!
overlays=uart0-m2 uart1-m1 uart3-m0 uart4-m0  # RESTART Linux !!!
overlays=lcd1 lcd2                            # RESTART Linux !!!
overlays=ov13850-c1                           # RESTART Linux !!!
bootlogo=false         #Turn off Logo         # RESTART Linux !!!
```

### orangepi-config (GPIO)
(Pag 252)

```bash
sudo orangepi-config
# System > Hardware > Choose and Restart Linux
```
![alt text](/Pictures/08.png)

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

1. Enalble PWM with [orangepiEnv](https://github.com/albertoRamon/OrangePi5B/blob/main/Hardware.md#orangepienv) 
2. Will appear more /dev/pwmchip<XX>
To know <XX> what PWM is related:
```bash
sys/class/pwm/ -l  #Check the link
```

* Files pwmchip<XX>
   * export
   * period
   * duty_cyple
   * enable
* TEST: Configure pwmchip<XX> 50 Hz (NO Symetric)
```bash
sudo su
echo 0 > /sys/class/pwm/pwmchip2/export
echo 20000000 > /sys/class/pwm/pwmchip2/pwm0/period
echo 1000000 > /sys/class/pwm/pwmchip2/pwm0/duty_cycle
echo 1 > /sys/class/pwm/pwmchip2/pwm0/enable
```

## SPI
(Pag 166)


1. Enalble SPI with [orangepiEnv](https://github.com/albertoRamon/OrangePi5B/blob/main/Hardware.md#orangepienv) 
2. Will appear more /dev/spidev<XX>.1  (Don't use XX.**0**)

* TEST:
   1. Connect PIN19 and PIN21 (MOSI and MISO of SPI4)
   2. RUN Script: The resutn Tx and Rx must be the same
```bash
   sudo spidev_test -v -D /dev/spidev4.1 --channel 4 --port 1
```


## I2C
(Pag 181)


|  I2C  |  NAME          | PIN                |
| ----- | -------------- |  ----------------- | 
| I2C1  | I2C1_SDA_M<X>  | 12 (M2) or 16 (M4) |
| I2C1  | I2C1_SCL_M<X>  | 15 (M2) or 18 (M4) |
| I2C3  | I2C3_SDA_M0    | 21  |
| I2C3  | I2C3_SCL_M0    | 19  |
| I2C5  | I2C5_SDA_M3    | 03  |
| I2C5  | I2C5_SCL_M3    | 05  |

Use Vcc (PIN 1) and Gnd (PIN 6)

1. Enalble I2C with [orangepiEnv](https://github.com/albertoRamon/OrangePi5B/blob/main/Hardware.md#orangepienv) 
2. Will appear more /dev/i2c-<XX>
3. Connect I2C device
4. Run Script:
```bash
   sudo i2cdetect -y 1 				#i2c1 command
   sudo i2cdetect -y 3 				#i2c3 command
   sudo i2cdetect -y 5 				#i2c5 command
```

## CAN

## UART
(Pag 169)

|  UART  |  NAME         | PIN   |
| ----- | -------------- |  ---- | 
| UART0  | UART0_TX_M2   | 08 |
| UART0  | UART0_RX_M2   | 10 |
| UART1  | UART1_TX_M1   | 05 |
| UART1  | UART1_RX_M1   | 03 |
| UART3  | UART3_TX_M0   | 19 |
| UART3  | UART3_RX_M0   | 21 |
| UART4  | UART4_TX_M0   | 18 |
| UART4  | UART4_RX_M0   | 16 |

1. Enalble UART with [orangepiEnv](https://github.com/albertoRamon/OrangePi5B/blob/main/Hardware.md#orangepienv) 
2. Will appear more /dev/ttyS<XX>
3. Run Script:
```bash
sudo gpio serial /dev/ttyS0
```


## MIPI LCD
(Pag 251)

1. Enalble LCD with [orangepiEnv](https://github.com/albertoRamon/OrangePi5B/blob/main/Hardware.md#orangepienv) 
2. If you connect an Screen, you must see Ubuntu Desktop (vertical configuration)


## MIPI Camera
(Pag 259)