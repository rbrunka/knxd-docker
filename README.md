# knxd-docker
knxd in docker

Raspberry Pi4 mit 8GB RAM + Weinzierl 838 KNX BAOS + Docker

Die Schritte:
1. BAOS-Modul anschliessen und Strom anschalten.
2. Service serial-getty@ttyS0.service abschalten:
Code:
sudo systemctl stop serial-getty@ttyS0.service
sudo systemctl disable serial-getty@ttyS0.service
sudo systemctl mask serial-getty@ttyS0.service
3. Neue Datei /etc/udev/rules.d/10-local.rules erstellen:
Code:
KERNEL=="ttyS0", SYMLINK+="serial0" GROUP="tty" MODE="0660"
KERNEL=="ttyAMA0", SYMLINK+="serial1" GROUP="tty" MODE="0660"
4. udev neu einlesen:
Code:
sudo udevadm control --reload-rules && sudo udevadm trigger
5. Zeichenkette
console=serial0,115200
von der Datei /boot/firmware/cmdline.txt entfernen.
Bei mir sieht die Datei jetzt so aus:
Code:
#net.ifnames=0 dwc_otg.lpm_enable=0 console=serial0,115200 console=tty1 root=LABEL=writable rootfstype=ext4 elevator=deadline rootwait fixrtc
net.ifnames=0 dwc_otg.lpm_enable=0 console=tty1 root=LABEL=writable rootfstype=ext4 elevator=deadline rootwait fixrtc
6. Bluetooth muss in der Datei /boot/firmware/usercfg.txt abgeschaltet werden:
Code:
# Place "config.txt" changes (dtparam, dtoverlay, disable_overscan, etc.) in
# this file. Please refer to the README file for a description of the various
# configuration files on the boot partition.

dtoverlay=disable-bt
7. docker-compose up -d
