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
