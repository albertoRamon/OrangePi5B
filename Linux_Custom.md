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
(Pag 101)
### Wired
```bash
ip addr show eth0
sudo ifconfig
ping www.baidu.com -I eth0
```

### Wifi CLI

|  **Don't use /etc/network/interfaces** |
| --- | 

(Pag 103), Bash only
```bash
nmcli dev wifi			#List hotspots
nmcli dev wifi connect wifi_name password wifi_passwd
```

(Pag 105), Use NCurses
```bash
nmtui
# Activate a connection
```

Test Connection
```bash
ip addr show wlan0		#See config
ping www.orangepi.org -I wlan0
```

(Pag 118), define static adress Bash only
```bash
nmtui  con show  AQUI !!!
# Activate a connection
```

(Pag 111), define static adress NCurses
```bash
nmtui
# Edit connection > Ethernet | Wifi > IP Config:  > Show
# After the changes the interfaz need Deactivata & Activate
```

### SSH
(Other option is use Debug)
(pag 127)

```bash
ssh root@192.168.1.xxx
reset_ssh.sh
```

### Debug
(Pag 81)
* Need a conversor TTL to USB at 1500000 bauds