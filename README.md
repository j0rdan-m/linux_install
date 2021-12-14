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
sudo apt install -y git dkms flameshot remmina stacer vim vlc gimp gnome-tweak-tool
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

Discord : (deb or tar.gz : https://discord.com/download)

vscode : https://code.visualstudio.com/download

balena etcher : https://www.balena.io/etcher/

## Citrix Workspace

### Download

Citrix Workspace : https://www.citrix.com/fr-fr/downloads/workspace-app/linux/workspace-app-for-linux-latest.html

### Certificate management


For SBM : 

  * Fedora: 

On firefox, download the PEM GlobalSign Root CA.  
Copy it on /opt/Citrix/ICAClient/keystore/cacerts/  
run ```sudo ./ctx_rehash``` on /opt/Citrix/ICAClient/util

  * Ubuntu : 

run ```sudo cp /usr/share/ca-certificates/mozilla/*.crt /opt/Citrix/ICAClient/keystore/cacerts/```

  * Manual download : https://www.tbs-certificats.com/FAQ/fr/gsgccr3dvtlsca2020.html

## Microsoft fonts

```sudo apt-get install fontforge cabextract```

```wget https://gist.github.com/maxwelleite/10774746/raw/ttf-vista-fonts-installer.sh -q -O - | sudo bash```

## Tips

### update-host alias

```alias update-host="sudo apt update && sudo apt upgrade -y && sudo apt dist-upgrade -y && sudo apt autoremove -y"```
