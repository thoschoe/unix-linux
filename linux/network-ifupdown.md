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
eth0
  address: 192.168.0.1
  netmask: 255.255.255.0
  gateway: 192.168.0.1
  dns
```
