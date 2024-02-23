# Ubuntu DHCP Client Status

Im Beispiel hat der Netzwerkadapter den Namen eth0.
Bei heutigen Linux-Distributionen wird Consistent Network Device Naming
oder auch biosdevicename verwendet - daher kann der Name abweichend sein.
(Z. B. mit dem Kommanodo "ip link" werden u. a. die Netzwerkadapter aufgelistet.)


```bash
# Allgemein:
cat /var/lib/dhcp/dhclient.eth0.leases

# Lease erneuern:
dhclient -v -4

# ifupdown:
ifconfig eth0 dhcp status

# netplan:
netplan ip leases eth0

# NetworkManager (Beispiel):
cat /var/lib/NetworkManager/internal-6604b755-b04f-33a3-8a74-8eec86f491b6-eth0.lease

# DHCP-Journal-Infos:

# Allgemein:
journalctl | grep -Ei 'dhcp'

# Networkd:
journalctl -u systemd-networkd | grep 'DHCPv4'

# NetworkManager:
journalctl -u NetworkManager | grep 'dhcp4'
```
Hinweis:  
Bei neueren Linux-Distributionen wird die IP-Adresse von Windows-DHCP-Servern
nicht anhand der Mac-Adresse, sondern anhand einer Machine-ID vergeben.

Das Verhalten kann man unter Netplan wie folgt aendern:

```bash
# Root-Shell
sudo -i
# Netplan Konfigurationsdatei editieren
vim /etc/netplan/00-installer.yaml
```
```yaml
#Netplan DHCP per Mac-Adresse:
network:
  ethernets:
    enp0s3:
      dhcp4: true
      dhcp-identifier: mac
  version: 2
```
```bash
netplan generate
netplan apply
```
Achtung:  
Beim Klonen von Virtuellen Machinen (VM) mit DHCP per Machine-ID
muss diese auf dem Klon neu generiert werden, weil dieser 
sonst die gleiche IP-Adresse wie die Quell-VM zugewiesen bekommt.
Dazu sollte die VM nach dem Klonen vorerst ohne Netzerkverbindung
gestartet werden.

Neu generieren der Machine-ID

```bash
# Root-Shell
sudo -i
# Machine-ID löschen
rm /etc/machine-id
# neu generieren
systemd-machine-id-setup
```
Ubuntu 20.04 enthaelt bzgl. der Machine-ID einen Bug, je nach dem mit welchem Release-ISO installiert wurde.
Die Datei machine-id liegt unter /etc und unter /var/lib/dbus existiert ein symbolischer Link auf diese.
Es kann bei Ubuntu 20 vorkommen, dass /var/lib/dbus/machine-id kein Link sondern eine Kopie der Datei unter /etc ist.
In diesem Fall greift die Erneuerung nicht - deshalb sollte dies vorsichtshalber geprueft werden

```bash
# Machine ID unter /var/lib/dbus pruefen

# Root-Shell
sudo -i
# Falsch unter Ubuntu 20:
ls -l /var/lib/dbus/machine-id 
-rw-r--r-- 1 root root ... /var/lib/dbus/machine-id
ls -l /etc/machine-id 
-r--r--r-- 1 root root ... /etc/machine-id
# Berichtigen:
rm /var/lib/dbus/machine-id
# Symlink erzeugen
ln -s /etc/machine-id /var/lib/dbus/machine-id
# pruefen
ls -l /var/lib/dbus/machine-id
lrwxrwxrwx 1 root root ... /var/lib/dbus/machine-id2 -> /etc/machine-id
```