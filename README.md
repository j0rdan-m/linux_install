# linux_install

## Wi-Fi dongle

### Back to last ok kernel (Fedora)

Install the kernel

```
sudo dnf install kernel-*-5.8.15
```

Find the kernel component

```
rpm -qa kernel\* |sort -V
```

reInstall all the kernel components

```
sudo dnf reinstall -y kernel-5.8.15-301.fc33.x86_64 kernel-core-5.8.15-301.fc33.x86_64 kernel-debug-5.8.15-301.fc33.x86_64 kernel-debug-core-5.8.15-301.fc33.x86_64 kernel-debug-devel-5.8.15-301.fc33.x86_64 kernel-debug-modules-5.8.15-301.fc33.x86_64 kernel-debug-modules-extra-5.8.15-301.fc33.x86_64 kernel-debug-modules-internal-5.8.15-301.fc33.x86_64 kernel-devel-5.8.15-301.fc33.x86_64 kernel-modules-5.8.15-301.fc33.x86_64 kernel-modules-extra-5.8.15-301.fc33.x86_64 kernel-modules-internal-5.8.15-301.fc33.x86_64
```

Downgrade

```
sudo dnf downgrade kernel
```

Avoid kernel update: Add ```exclude=kernel*``` to the file /etc/dnf/dnf.conf

### Install wifi dongle drivers

```
sudo apt update && sudo apt install git -y

git clone "https://github.com/RinCat/RTL88x2BU-Linux-Driver.git"
cd RTL88x2BU-Linux-Driver
make clean
make
sudo make install
```

#### Old version

if needed, uninstall the previous driver : `sudo dkms remove rtl88x2bu/5.8.7.4 --all
`

```
git clone https://github.com/cilynx/rtl88x2bu.git
cd rtl88x2bu
VER=$(sed -n 's/\PACKAGE_VERSION="\(.*\)"/\1/p' dkms.conf)
sudo rsync -rvhP ./ /usr/src/rtl88x2bu-${VER}
sudo dkms add -m rtl88x2bu -v ${VER}
sudo dkms build -m rtl88x2bu -v ${VER}
sudo dkms install -m rtl88x2bu -v ${VER}
sudo modprobe 88x2bu
```

### Install bluetooth dongle

Download the drivers here : https://www.xmpow.com/pages/download

Get the MPOW BH456A one

(if still available : `wget https://mpow.s3-us-west-1.amazonaws.com/20201202_mpow_BH456A_driver+for+Linux.7z` )

Then unzip the 20201202_mpow_BH456A_driver+for+Linux.7z files (version coudl change)

```
cd  20201202_LINUX_BT_DRIVER/usb
(if needed :)sudo apt install gcc
sudo make install
cd..
sudo cp rtkbt-firmware/lib/firmware/rtl8761bu_fw /lib/firmware/
sudo cp rtkbt-firmware/lib/firmware/rtl8761bu_config /lib/firmware/

```

### Bluetooth update for MX Keys mini

```
cd /lib/firmware/brcm && sudo wget https://github.com/winterheart/broadcom-bt-firmware/raw/master/brcm/BCM20702A1-0a5c-21e8.hcd
```

Remove and re-plug the dongle

```
bluetoothctl connect CB:DD:B4:5C:4E:E3
bluetoothctl trust CB:DD:B4:5C:4E:E3
bluetoothctl pair CB:DD:B4:5C:4E:E3
```

## bitwarden extension

go there : 
  * [bitwarden](https://addons.mozilla.org/en-US/firefox/addon/bitwarden-password-manager/?utm_source=addons.mozilla.org&utm_medium=referral&utm_content=search)

## gnome

  * [gnome shell extension](https://extensions.gnome.org/)
  * ```sudo dnf install gnome-tweak-tool```
  * ```sudo apt install gnome-tweak-tool```

### themes

  * gnome application : https://www.gnome-look.org/p/1297346/
  * gnome shell : https://www.gnome-look.org/p/1013030/
  
### extensions

  * https://extensions.gnome.org/extension/2890/tray-icons-reloaded/
  * https://extensions.gnome.org/extension/307/dash-to-dock/
  * https://extensions.gnome.org/extension/906/sound-output-device-chooser/
  
## From package manager

### apt

```
sudo apt install -y git dkms flameshot remmina stacer vim vlc gimp blueman fonts-firacode baobab flatpak crowdsec docker.io docker-compose-v2 filezilla
sudo add-apt-repository ppa:solaar-unifying/ppa -y && sudo apt update && sudo apt install solaar -y
```

### dnf

```
sudo dnf install -y https://download1.rpmfusion.org/free/fedora/rpmfusion-free-release-$(rpm -E %fedora).noarch.rpm
sudo dnf install -y git dkms flameshot remmina stacer vim vlc gimp
```

## Package download

Teams : https://www.microsoft.com/fr-fr/microsoft-365/microsoft-teams/download-app

Slack : https://slack.com/intl/fr-fr/downloads/linux

Zoom : https://zoom.us/download?os=linux

Cozy Drive : https://docs.cozy.io/en/howTos/sync/linux/

pcloud : https://www.pcloud.com/fr/how-to-install-pcloud-drive-linux.html

WPS : https://linux.wps.com/

Signal : https://signal.org/fr/download/linux/

vscode : https://code.visualstudio.com/download

balena etcher : https://www.balena.io/etcher/

appImageLauncher : https://github.com/TheAssassin/AppImageLauncher/releases

zed : 
```
curl -sS https://debian.griffo.io/EA0F721D231FDD3A0A17B9AC7808B4DD62C41256.asc | sudo gpg --dearmor --yes -o /etc/apt/trusted.gpg.d/debian.griffo.io.gpg
echo "deb https://debian.griffo.io/apt jammy main" | sudo tee /etc/apt/sources.list.d/debian.griffo.io.list
sudo apt update
```

### Security

Portmaster : https://safing.io/
ProtonVPN : https://protonvpn.com/support/fr/official-linux-vpn-ubuntu
Windscribe : https://fra.windscribe.com/download/


## Citrix Workspace

### Download

Citrix Workspace : https://www.citrix.com/fr-fr/downloads/workspace-app/linux/workspace-app-for-linux-latest.html

### Certificate management

  * Fedora: 

On firefox, download the PEM GlobalSign Root CA.  
Copy it on /opt/Citrix/ICAClient/keystore/cacerts/  
run ```sudo ./ctx_rehash``` on /opt/Citrix/ICAClient/util

  * Ubuntu : 

run ```sudo cp /usr/share/ca-certificates/mozilla/*.crt /opt/Citrix/ICAClient/keystore/cacerts/```

  * Manual download : https://www.tbs-certificats.com/FAQ/fr/gsgccr3dvtlsca2020.html

## Microsoft fonts

```
sudo apt-get install fontforge cabextract
wget https://gist.github.com/maxwelleite/10774746/raw/ttf-vista-fonts-installer.sh -q -O - | sudo bash
wget http://download.tuxfamily.org/polyglotte/archives/msfonts-config2.zip
sudo unzip msfonts-config2.zip -d /etc/fonts/
```

## JetBrains fonts

```
wget https://download.jetbrains.com/fonts/JetBrainsMono-2.242.zip
unzip JetBrainsMono-2.242.zip
cd fonts/ttf
sudo mv JetBrainsMono-*.ttf /usr/share/fonts/
```

