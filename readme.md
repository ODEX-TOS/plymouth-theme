# plymouth theme

This theme is made for tos plymouth

## prerequisites

Perform the following actions so that plymouth can be displayed on the screen during boot

1. Install plymouth
```bash
yay -S plymouth
```
2. Update `/etc/mkinitcpio.conf`
```bash
HOOKS="... plymouth" # add plymouth to the end
```
3. Update mkinitcpio
```bash
sudo mkinitcpio -p linux-tos
```
4. Update grub config `/etc/default/grub`
```bash
GRUB_CMDLINE_LINUX_DEFAULT="... quiet splash vt.global_cursor_default=0"
```
5. Update grub
```bash
sudo grub-mkconfig -o /boot/grub/grub.cfg
```
6. Setup plymouth for your Display Manager
```bash
sudo systemctl disable lightdm
sudo systemctl enable  lightdm-plymouth
```

## Install theme

First we put this theme in the correct location
```bash
sudo mkdir -p /usr/share/plymouth/themes/tos
sudo cp * /usr/share/plymouth/themes/tos/
```

Now we can change the default theme to the one provided by TOS.
Do this by editing this file: `/etc/plymouth/plymouthd.conf`
```ini
[Daemon]
Theme=tos
ShowDelay=1
```


After changing the theme rebuild your initial ramdisk to hold the latest changes:
```bash
sudo mkinitcpio -p linux-tos
```
