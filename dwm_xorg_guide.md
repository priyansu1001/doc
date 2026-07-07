# try avoiding aur, and going full pacman (for safety)

# basic need

```
sudo pacman -S git base-devel kitty xorg-server xorg-xinit bat ripgrep tealdeer zoxide mpv yazi htop btop imagemagick picom firefox eza linux-headers linux-lts-headers
```

# nvidia stuff

checking drivers
```
lspci -k | grep -A 3 -E "(VGA|3D)"
```

```
sudo pacman -S nvidia-open nvidia-utils nvidia-prime nvidia-settings 
```

## nvidia fyi
use either nvidia-open or whats the properitery option

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
