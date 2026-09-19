# Debian-Installing-Nvidia-drivers-the-hard-way
[Debian] Installing Nvidia drivers - the hard way

<b>[Optional]</b> Run System Update<br>
```bash
sudo apt update && apt dist-upgrade
sudo systemctl reboot
```

Install the Kernel Sources and Kernel Development<br>
```bash
sudo apt update && sudo apt install patch build-essential linux-headers-$(uname -r) dkms pkg-config libglvnd-dev
```

Disable Nouveau<br>
```bash
[Recommended] You can add the following parameters to your kernel command line: 
module_blacklist=nouveau,nova_core,nova_drm
update-grub

OR

cat <<EOF | sudo tee /etc/modprobe.d/blacklist-nouveau.conf
blacklist nouveau
options nouveau modeset=0
EOF
```

<b>[Optional]</b> During Grub boot up add the following to you kernel command line.<br>
```bash
nomodset 3
```

If your running NVIDIA 470
<pre>
https://github.com/joanbm/nvidia-470xx-linux-mainline
</pre>

sudo to root and run the NVIDIA installer<br>
```bash
sh NVIDIA*.run
```

-------------------------

Additional notes:

Switch to console (no X11 running):
```bash
sudo systemctl isolate multi-user.target
During blank screen, you may have to 'CTRL+ALT+F1' for console terminal.
```

Start X manually first if needed:
```bash
sudo systemctl isolate graphical.target
```

Make graphical default (after testing):
```bash
sudo systemctl set-default graphical.target
```




