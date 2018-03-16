# linux-tips
Tips on setting up a linux workstation /server.

## Fedora Workstation

### 1. Blocking Kernel Updates
- Block kernel updates from installing:
```
sudo echo "exclude=kernel*" >> /etc/dnf/dnf.conf 
```

- List all available boot entries:
```
sudo grep -P "submenu|^menuentry" /boot/efi/EFI/fedora/grub.cfg | cut -d "'" -f2
```

- Boot the desired kernel at startup:
```
sudo grub2-set-default "Fedora (4.13.9-300.fc27.x86_64) 27 (Twenty Seven)
```

### 2. Fix blank Wine applications (PlayOnLinux)
Problem as reported [here](https://askubuntu.com/questions/976300/installing-microsoft-office-2010-in-ubuntu-17-10-with-playonlinux-does-not-proce):

- Remove outdated libraries that ship with wine on playonlinux
```
rm ~/.PlayOnLinux/wine/linux*/*/lib*/libz*
```

### 3. WhatsApp Desktop Client
- Add [3rd party](https://github.com/Enrico204/Whatsapp-Desktop) repo:
```
sudo bash -c 'cat << EOF > /etc/yum.repos.d/Enrico204_Whatsapp-Desktop.repo
[Enrico204_Whatsapp-Desktop]
name=Enrico204_Whatsapp-Desktop
baseurl=https://packagecloud.io/Enrico204/Whatsapp-Desktop/el/6/$basearch
repo_gpgcheck=1
gpgcheck=0
enabled=1
gpgkey=https://packagecloud.io/Enrico204/Whatsapp-Desktop/gpgkey
sslverify=1
sslcacert=/etc/pki/tls/certs/ca-bundle.crt
metadata_expire=300
EOF'
```
- Enable and install app:
```
sudo dnf config-manager --set-enabled Enrico204_Whatsapp-Desktop -y
sudo dnf install  WhatsApp -y
```

### 4. Remmina Remote Desktop Client
- Add 3rd party repo:
```
sudo dnf copr enable hubbitus/remmina-next -y
```

- Install Reminna
```
sudo dnf upgrade --refresh 'remmina*' 'freerdp*'
sudo dnf install remmina*
```
