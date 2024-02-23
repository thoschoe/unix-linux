# Ubuntu Server - Hostnamen ändern

##### bis Ubuntu 14 (ohne systemd):
- Editieren der Datei /etc/hostname

##### ab Ubuntu 16 (mit systemd)
- Kommando hostnamectl

Beispiel:
```bash
# Anzeigen des Hostnamens (alt)
cat /etc/hostname
ubuntu-server.lan
# Anzeigen des Hostnamens (neu)
hostnamectl
   Static hostname: ubuntu-server.lan
         Icon name: computer-laptop
           Chassis: laptop
        Machine ID: xxxxxxxxxxxxxxxxxxxxx
           Boot ID: xxxxxxxxxxxxxxxxxxxxx
  Operating System: Ubuntu 20.04.2 LTS
            Kernel: Linux 5.4.0-80-generic
      Architecture: x86-64
# anderen Hostnamen setzten
hostnamectl set-hostname ubuntu.lan
# Hostnamen erneut ausgeben
cat /etc/hostname
ubuntu.lan
```
