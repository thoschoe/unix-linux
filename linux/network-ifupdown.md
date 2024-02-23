### Netzwerkkonfiguration mit ifupdown

```bash
# root-shell
sudo -i
# ipupdown installieren
apt-get install -y ifupdown
# ggf. netplan deinstallieren
apt-get purge -y netplan.io
# Datei /etc/network/interfaces editieren
vim /etc/network/interfaces
```
##### Statische IP-Adresse konfigurieren

```text
auto lo
iface lo inet loopback

auto eht0
iface eth0 inet static
  address 192.168.0.2
  netmask 255.255.255.0
  gateway 192.168.0.1
  dns-nameservers 1.1.1.1 8.8.8.8
  dns-search meinnetz.lan
```
Weiterführende Informationen:  
https://wiki.ubuntuusers.de/interfaces/
