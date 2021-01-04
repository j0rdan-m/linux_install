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

## bitwarden extension 

go there : 
  * [bitwarden](https://addons.mozilla.org/en-US/firefox/addon/bitwarden-password-manager/?utm_source=addons.mozilla.org&utm_medium=referral&utm_content=search)

## gnome

  * [gnome shell extension](https://extensions.gnome.org/)
  * ```sudo dnf install gnome-tweak-tool```
  
## From package manager

### apt

```
sudo apt install -y git dkms flameshot remmina stacer vim vlc gimp
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
