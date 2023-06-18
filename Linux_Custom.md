_Only custom commands/procedures for Orange PI_


# AutoLoging
(Pag 95)
Autologin CLI
```bash
sudo auto_login_cli.sh <NameUser>   #Enable
sudo auto_login_cli.sh -d			#Disable
```
Autologin Desktop
```bash
sudo disable_desktop_autologin.sh 	#Current user
sudo desktop_login.sh <NameUser>	#Any user
```

# Enable / Disable Desktop
(Pag 97)
```bash
sudo orangepi-config				
## System > Desktop > Stop | Enable
```