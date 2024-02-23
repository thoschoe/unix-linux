# Simple Network Messaging Protokol Daemon - snmpd

##### Installaiton

```bash
# Root-Shell
sudo -i
# Installation
apt-get install -y snmpd
# Wechsel in Konfigurationsverzeichnis
cd /etc/snmpd
# Backup Originalkonfig
cp snmpd.conf backup_snmpd.conf
# Neue einfache Konfig erstellen
vim snmpd.conf
rocommunity public 192.168.1.0/24
sysLocation "Zu Hause"
sysContact  "admin@meinnetz.lan"
sysName "Ubuntu Server"
# Dienst anpassen:
# SNMP-Zugriffe in eigene Logdatei statt systemd-journal
# Kopie der Orginalkonfig erstellen
cp /lib/systemd/system/snmpd.service /etc/systemd/system/snmpd.service
# Dienstkonfiguration editieren
vim /etc/systemd/system/snmpd.service
#Orginal:
#ExecStart=/usr/sbin/snmpd -Lsd -Lf /dev/null -u Debian-snmp -g Debian-snmp -I -smux,mteTrigger,mteTriggerConf -f
#Geändert:
#1. -Lsd entfernt --> schreibt nicht mehr in syslog 
#2. -Lf /dev/null in -Lf /var/log/snmpd.log ge<E4>ndert --> leitet in Logdatei um
#3. --logTimestamp=true hinzugef<FC>gt --> schreibt Zeitstempel in log-Datei
ExecStart=/usr/sbin/snmpd --logTimestamp=true -Lf /var/log/snmpd.log -u Debian-snmp -g Debian-snmp -I -smux,mteTrigger,mteTriggerConf -f
# Geänderte Konfiguration laden
systemctl daemon-reload
# Dienst neu starten
systemctl restart snmpd.service
# Log-Rotation für snmpd.log einrichten
# Logrotate-Konfiguraitonsdatei anlegen und editieren
vim /etc/logrotate.d/snmpd
/var/log/snmpd.log {
    daily
    missingok
    notifempty
    rotate 14
    compress
    dateext
    dateformat -%Y-%m-%d
}
```
##### SNMP testen
```bash
# snmpwalk installieren
apt-get install -y snmpwalk
# snmpwalk ausführen
snmpwalk ubuntu-server.lan
```
