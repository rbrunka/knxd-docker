# knxd-docker
knxd in docker

Raspberry Pi4 mit 8GB RAM + Weinzierl 838 KNX BAOS + Docker

Getestet mit Raspbian Lite (bullseye, 64bit)

Die Schritte:
1. BAOS-Modul anschliessen und Strom anschalten.

2. Docker (https://docs.docker.com/engine/install/debian/) und docker-compose (https://docs.docker.com/compose/install/) installieren 

3. `raspi-config` starten und:
`3. Interface Options -> Serial Port -> No -> Yes`

Der richtige Output ist:
The serial login shell is disabled
The serial interface is enabled

4. /etc/boot.config um volgende Zeilen erweitern:
<pre><code>
[all]
enable_uart=1
dtoverlay=disable-wifi
dtoverlay=disable-bt
</code></pre>

5. `reboot`

6. Das Repo clonen: `git clone https://github.com/rbrunka/knxd-docker.git`

Bei Bedarf die `knxd/entrypoint.sh` anpassen.
Nach jeder Anpassung `docker-compose build` nicht vergessen.

7. `docker-compose up -d`
Fertig.
