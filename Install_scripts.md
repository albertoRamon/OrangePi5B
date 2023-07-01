
# Install soft
```bash
sudo apt-get update
sudo apt-get upgrade  -y

sudo apt-get install git         -y
sudo apt-get install wget        -y
sudo apt-get install iproute2    -y
sudo apt-get install notepadqq   -y
sudo apt-get install filezilla   -y
sudo apt-get install glmark2     -y
sudo apt-get install default-jre -y
sudo apt-get install default-jdk -y
sudo apt-get install psensor     -y
sudo apt-get install lm-sensors  -y
sudo apt-get install chrome-gnome-shell -y

# Libreoffice
sudo add-apt-repository ppa:libreoffice/ppa  -y
sudo apt update -y
sudo apt-get install libreoffice -y

#veracrypt
sudo add-apt-repository ppa:unit193/encryption  -y
sudo apt-get update
sudo apt install veracrypt -y
```


### Install firefox (deb Package)
```bash
sudo snap remove firefox
sudo add-apt-repository ppa:mozillateam/ppa  -y
sudo apt-get update

echo '
Package: *
Pin: release o=LP-PPA-mozillateam
Pin-Priority: 1001

Package: firefox
Pin: version 1:1snap1-0ubuntu2
Pin-Priority: -1
' | sudo tee /etc/apt/preferences.d/mozilla-firefox

echo 'Unattended-Upgrade::Allowed-Origins:: "LP-PPA-mozillateam:${distro_codename}";' | sudo tee /etc/apt/apt.conf.d/51unattended-upgrades-firefox

sudo apt install firefox -y --allow-downgrades
```


### Azure CLI [Link](https://learn.microsoft.com/en-us/cli/azure/install-azure-cli-linux?pivots=apt#option-2-step-by-step-installation-instructions)
```bash
sudo apt-get install ca-certificates curl apt-transport-https lsb-release gnupg -y
sudo mkdir -p /etc/apt/keyrings
curl -sLS https://packages.microsoft.com/keys/microsoft.asc |
    gpg --dearmor |
    sudo tee /etc/apt/keyrings/microsoft.gpg > /dev/null
sudo chmod go+r /etc/apt/keyrings/microsoft.gpg
AZ_REPO=$(lsb_release -cs)
echo "deb [arch=`dpkg --print-architecture` signed-by=/etc/apt/keyrings/microsoft.gpg] https://packages.microsoft.com/repos/azure-cli/ $AZ_REPO main" |
    sudo tee /etc/apt/sources.list.d/azure-cli.list
sudo apt-get update
sudo apt-get install azure-cli  -y
```

### Visual Studio Code
[Download](https://code.visualstudio.com/download)

### Azure Data Studio
[Download](https://learn.microsoft.com/en-us/sql/azure-data-studio/download-azure-data-studio?view=sql-server-ver16&tabs=redhat-install%2Credhat-uninstall#download-azure-data-studio)
Unfortunally there is no version ARM64 for Linux


### Azure Storage Explorer
[Download](https://github.com/microsoft/AzureStorageExplorer/releases)
Unfortunally there is no version ARM64 for Linux


### Postman
```bash
wget https://dl.pstmn.io/download/latest/linux_arm64
```


### gNome
[extensions.gnome.](https://extensions.gnome.org/)
* [system-monitor-next](https://extensions.gnome.org/extension/3010/system-monitor-next/)
* [applications-menu](https://extensions.gnome.org/extension/6/applications-menu/)
* [removable-drive-menu](https://extensions.gnome.org/extension/7/removable-drive-menu/)
* [allow-locked-remote-desktop](https://extensions.gnome.org/extension/4338/allow-locked-remote-desktop/)
* [screenshot-tool](https://extensions.gnome.org/extension/1112/screenshot-tool/)


```bash


```


```bash


```