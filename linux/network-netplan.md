### Netzwerkkonfiguration mit netplan unter Ubuntu Server ab 18.04

```bash
# root-shell
sudo -i
# ggf. netplan installieren
apt-get install -y netplan.io
# in netplan konfigurationsverzeichnis wechseln
cd /etc/netplan
# Konfiguraiton erstellen
# Es können mehrere Konfigurationsdateien existieren.
# Die mit der höchsten vorangestellten Nummer wird genommen.
# In der Regel ist die Datei 00-installer.yaml mit DHCP-Konfiguration vorhanden.
# Beispiel: Konfiguation mit Editor VIM erstellen:
vim 01-netcfg.yaml
```
Die Konfigruationsdatei muss im YAML-Format erstellt werden.  
Die Einrückung in der Konfiguration ist zwingend zu beachten!

```yaml
network:
  version: 2
  renderer: networkd
  ethernets:
    eth0:
      dhcp4: no
      dhcp6: no
      # Mehrere IP-Adressen können duch Komma getrennt angegeben werden
      addresses: [192.168.0.1/24]
      gateway4: 192.168.0.1
      dns-namservers:
        search: 
        nameservers: [1.1.1.1,8.8.8.8]
```

