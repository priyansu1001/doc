# try avoiding aur, and going full pacman (for safety)

# connect to wifi

```
systemctl start iwd
iwctl
station list
station wlan0 scan
station wlan0 get-networks
station wlan0 connect 'Network'
```

# basic need

```
sudo pacman -S git base-devel kitty xorg-server xorg-xinit bat ripgrep tealdeer zoxide mpv yazi htop btop imagemagick picom eza linux-headers linux-lts-headers archlinux-keyring firefox nitrogen rofi nomacs flameshot xclip noto-fonts-cjk noto-fonts-emoji termdown```

# amd stuff 

These might be installed already, ifit did, no need
test if lib32-mesa vulkan-radeon lib32-vulkan-radeon are needed or not
```
sudo pacman -S mesa lib32-mesa vulkan-radeon lib32-vulkan-radeon
```

# nvidia stuff

checking drivers
```
lspci -k | grep -A 3 -E "(VGA|3D)"
```

```
sudo pacman -S nvidia-open nvidia-utils nvidia-prime nvidia-settings 
```

use either nvidia-open or aur version

add this
```
nvidia_drm.modeset=1 
```
to your 
```
/etc/default/grub
```
then 
```
sudo grub-mkconfig -o /boot/grub/grub.cfg
```
the grub file should be like this
```
GRUB_DEFAULT=0
GRUB_TIMEOUT=5
GRUB_DISTRIBUTOR=`( . /etc/os-release; echo ${NAME:-Kali} ) 2>/dev/null || echo Kali`
GRUB_CMDLINE_LINUX_DEFAULT="nvidia_drm.modeset=1"
GRUB_CMDLINE_LINUX=""
```

According to the NVIDIA developer zone: Create a file:

```
sudo nano /etc/modprobe.d/blacklist-nouveau.conf
```

With the following contents:

```
blacklist nouveau 
options nouveau modeset=0
```

Regenerate the kernel initramfs:

```
sudo update-initramfs -u
```

Finally, reboot:

```
sudo reboot
```

# xinitrc file

```
exec dwm
picom
```

# Autostart X at login

Place the following in your login shell initialization file (e.g. ~/.bash_profile for Bash or ~/.zprofile for Zsh):

```
if [ -z "$DISPLAY" ] && [ "$XDG_VTNR" -eq 1 ]; then
  exec startx
fi
```

You can replace the `-eq` comparison with one like `-le 3` (for vt1 to vt3) if you want to use graphical logins on more than one virtual terminal.

Alternative conditions to detect the virtual terminal include `"$(tty)" = "/dev/tty1"`, which does not allow comparison with `-le`, and `"$(fgconsole 2>/dev/null || echo -1)" -eq 1`, which does not work in serial consoles.

The exec command ensures that the user is logged out when the X server exits, crashes or is killed by an attacker. If you want to take the risk and remain logged in when the X session ends, remove exec.



# DWM keybind cheatsheet
Basic
=====

[Shift]+[Mod]+[Enter]   - launch terminal.

[Mod]+[b]               - show/hide bar.
[Mod]+[p]               - dmenu for running programs like the x-www-browser.
[Mod]+[Enter]           - push acive window from stack to master, or pulls last used window from stack onto master.

[Mod] + [j / k]         - focus on next/previous window in current tag.
[Mod] + [h / l]         - increases / decreases master size.

Navigation
==========

[Mod]+[2]               - moves your focus to tag 2.
[Shift]+[Mod]+[2]       - move active window to the 2 tag.

[Mod] + [i / d]         - increases / decreases number of windows on master
[Mod] + [, / .]         - move focus between screens (multi monitor setup)
[Shift]+[Mod]+[, / .]   - move active window to different screen.

[Mod]+[0]               - view all windows on screen.
[Shift]+[Mod]+[0]       - make focused window appear on all tags.
[Shift]+[Mod]+[c]       - kill active window.
[Shift]+[Mod]+[q]       - quit dwm cleanly.

Layout
======

[Mod]+[t]               - tiled mode. []=
[Mod]+[f]               - floating mode. ><>
[Mod]+[m]               - monocle mode. [M] (single window fullscreen)

Floating
========

[Mod]+[R M B]           - to resize the floating window.
[Mod]+[L M B]           - to move the floating window around.
[Mod]+[Space]           - toggles to the previous layout mode.
[Mod]+[Shift]+[Space]   - to make an individual window float.
[Mod]+[M M B]           - to make an individual window un-float.
