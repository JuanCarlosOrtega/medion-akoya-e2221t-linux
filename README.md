# medion-akoya-e2221t-linux
Linux configurations to make the laptop Medion Akoya E2221T usable in Linux

## Disable Suspend target in systemd
As root user, type the following command to disable suspend.target goal of systemd:
```
# systemctl mask suspend.target
```
This change will solve random laptop suspend states.

## Disable logind suspend events from hardware
As root user, edit the logind.conf file to tune some tricky parameters related to laptop lid switch:
```
# nano /etc/systemd/logind.conf 
```

Uncomment the following line and set ignore value:
```
HandleSuspendKey=ignore
HandleLidSwitch=ignore
```
This change will solve the high cpu usage of the suspend and lid switch events that affects logind systemd services.

## Avoid Gnome software to be launched every time
To avoid high memory usage in a computer that has only 4Gb of Ram with four Intel Atom cores, the solution is to override the default system autostart scripts for our own user.

Inside your local user folder type the following commands:
```
$ cd .config/
$ mkdir autostart
$ cd autostart/
$ cp /etc/xdg/autostart/org.gnome.Software.desktop .
$ nano org.gnome.Software.desktop 
```

Put the following line at the end of the file:
```
X-GNOME-Autostart-enabled=false
```
Finally save and reboot your system. After this configuration the laptop will show near 0% CPU usage in idle. Also the RAM usage will be decreased in about 300Mb, using Fedora 39 and Gnome Shell desktop.

Enjoy!
