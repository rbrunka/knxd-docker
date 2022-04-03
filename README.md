# knxd-docker
knxd in docker

Raspberry Pi4 mit 8GB RAM + Weinzierl 838 KNX BAOS + Docker

Getestet mit Raspbian Lite (bullseye, 64bit)

Die Schritte:
1. BAOS-Modul anschliessen und Strom anschalten.

2. Docker und docker-compose installieren

3. `raspi-config` starten und:
`3. Interface Options -> Serial Port -> No -> Yes`

Der richtige Output ist:
`The serial login shell is disabled                       │
The serial interface is enabled`

4. /etc/boot.config um volgende Zeilen erweitern:
`[all]
enable_uart=1
dtoverlay=disable-wifi
dtoverlay=disable-bt`

5. `reboot`

4. Das Repo clonen: `git clone https://github.com/rbrunka/knxd-docker.git`

7. `docker-compose up -d`

**
Bei Bedarf die `entrypoint.sh` anpassen.
