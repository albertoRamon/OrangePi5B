_Only custom commands/procedures for Orange PI_


# AutoLoging
(Pag 95)
Autologin CLI
```bash
sudo auto_login_cli.sh <NameUser>   	#Enable
sudo auto_login_cli.sh -d			#Disable
```
Autologin Desktop
```bash
sudo disable_desktop_autologin.sh 	#Current user
sudo desktop_login.sh <NameUser>	#Any user
```

# Enable / Disable Desktop Service
(Pag 97)
```bash
sudo orangepi-config				
## System > Desktop > Stop | Enable
```


# Networking
|  **Don't use /etc/network/interfaces** |
| --- | 

### Configuration Bash only

* Configure Wifi: (Pag 103)
```bash
nmcli dev wifi			#List hotspots
nmcli dev wifi connect wifi_name password wifi_passwd
```

* Put fix IP: (Pag 118)
```bash
nmtui con show  						#See config
nmcli con mod "Wired connection 1" 	\	#Config Wifi
   ipv4.addresses "192.168.1.110" 	\
   ipv4.gateway "192.168.1.1" 		\
   ipv4.dns "8.8.8.8" 				\
   ipv4.method "manual"

nmcli con mod "orangepi"				#Config Lan
   ipv4.addresses "192.168.1.110" 	\
   ipv4.gateway "192.168.1.1" 		\
   ipv4.dns "8.8.8.8" 				\
   ipv4.method "manual"

sudo reboot
```


### Configuration NCurses

* Configure: (Pag 105, 111)
```bash
nmtui
# Activate a connection
```
* Put fix IP:
```bash
nmtui
# Edit connection > Ethernet | Wifi > IP Config:  > Show
# After the changes the interfaz need Deactivata & Activate
```

### Test Connection
```bash
sudo ifconfig			#See config
ip addr show wlan0		#See config
ip addr show eth0		#See config

ping www.orangepi.org -I wlan0
ping www.orangepi.org -I eth0
```

### SSH
(Other option is use Debug)
(pag 127)

```bash
ssh root@192.168.1.xxx
reset_ssh.sh			#If remote SSH is not working
```


### ADB
(Pag. 130)

### Debug
(Pag 81)
* Need a conversor TTL to USB at 1500000 bauds