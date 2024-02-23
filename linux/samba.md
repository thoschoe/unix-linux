# SAMBA - Filesharing per SMB

- - -

### Installation

```bash
# Root-Shell
sudo -i
# Samba installieren
apt-get install -y samba
# Für jeden Nutzer der auf Feigaben zugreifen soll,
# muss noch ein zusätzlichen SAMBA-Kennwort vergeben werden
smbpasswd -a Benutername
# Anpassungen
# Datei /etc/samba/smb.conf editieren
vim /etc/samba/smb.conf
```
Beispiel Freigabe in smb.conf:

```cfg
[freigabe]
    comment = Freigabe
    path = /media/freigabe
    browsable = yes
    create mask = 0664
    directory mask = 0775
    writable = yes
    guest ok = no
    valid users = @linuxnutzer
    hosts allow = 192.168.0.2
```

##### Freigabe auf der Shell beim Client einbinden

Variante 1:

```bash
# Root-Shell
sudo -i
# SMB-Client installieren
apt-get install smbclient -y
# ggf. lokales Verzeichnis anlegen
mkdir /media/freigabe
# Freigabe aufrufen
smbclient -U username //server/freigabe
# Domänen-Freigabe aufrufen
smbclient -U username -W domain.net //server/freigabe
```

Variante 2:

```bash
# Root-Shell
sudo -i
# cifs installieren
apt-get install cifs-utils
# ggf. lokales Verzeichnis anlegen
mkdir /media/freigabe
# Freigabe mit smbmount einbinden
smbmount //server/freigabe /media/freigabe/ -o user=domain/user
```

##### Freigaben im grafischen Dateimanager aufrufen

```bash
# Installation gvfs-backends
apt-get install -y gvfs-backends
```
##### Freigabe im Dateimanager aufrufen

`smb://server/freigabe`

##### Freigabe dauerhaft mounten und bei Verlust der Netzwerkverbindung automaitsch wieder einbinden

```bash
# Installation Samba-Clientsoftware
apt-get install cifs-utils

# fstab bearbeiten
vim /etc/fstab

# anfügen:
# SMB-Mount auf Dateiserver
//server/freigabe /media/feigabe cifs rw,credentials=/root/.smb-cred,uid=1000,forceuid,gid=1000,forcegid,addr=192.168.0.2,file_mode=0664,dir_mode=0775,x-systemd.automount,x-systemd.requires=network-online.target 0 0

vim /root/.smb-cred
# Linux-Nutzer mit der User-ID 1000
username=linuxnutzer
password=smbpasswort-von-linuxnutzer

# Freigabe einhaengen (mounten)
mount /media/freigabe
```
Rückgängig machen:
- Freigabe aushaengen ( `umount /media/freigabe` )
- Konfigurationszeile aus /etc/fstab entfernen

```bash
# Clientsoftware deinstallieren
apt-get purge -y  cifs-utils
# Nicht mehr benötigte Abhängigkeiten deinstallieren
apt-get autoremove -y
```
Links:
- https://wiki.ubuntuusers.de/Samba_Server/
- https://wiki.ubuntuusers.de/Samba_Server/smb.conf/
- https://www.thomas-krenn.com/de/wiki/Windows_Freigabe_unter_Linux_mounten
- https://linuxwiki.de/smbclient
