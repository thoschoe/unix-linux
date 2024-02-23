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
# Die Konfigurationsdateien werden nach der Nummerierungsreihenfolge abgearbeitet.
# In der Regel ist die Datei 00-installer.yaml mit DHCP-Konfiguration vorhanden.
# Diese sollte nach Erstellen der Static-IP-Konfigurationsdatei entfernt werden.
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
      addresses: [192.168.0.2/24]
      gateway4: 192.168.0.1
      namservers:
        addresses: [1.1.1.1,8.8.8.8]
```
Ab Ubuntu 22 ist die Konfiguration leicht abweichend:

```yaml
network:
  renderer: networkd
  ethernets:
    eth0:
      addresses:
        - 192.168.0.2/24
      nameservers:
        addresses: [1.1.1.1,8.8.8.8]
      routes:
        - to: default
          via: 192.168.0.1
  version: 2
```

Konfiguration übernehmen:
```bash
# Konfiguration generieren
# Ggf. auf Fehlermeldungen achten!
netplan generate
# Konfiguration übernehmen
netplan apply
```
Ab Ubuntu 22 erfolgt eine Warnmeldung, dass die Konfigurationsdatei zu viele Rechte besitzt.  
Abhilfe (als root):
```bash
# Rechte der Konfigurationsdatei auf user root einschaenken
chmod 600 /etc/netplan/01-netcfg.yaml
```

Weiterführende Informationen:  
https://wiki.ubuntuusers.de/Netplan/
