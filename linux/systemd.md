# systemd

#### Beispiele Kommandos:

```bash
# ggf. Root-Shell starten
sudo -i
# Status des Systems anzeigen
systemctl status
# Status eines Dienstes (Unit) anzeigen
systemctl status dienst.service
# Dienst stoppen
systemctl stop dienst.service
# Dienst starten
systemctl start dienst.service
# Konfiguration neu einlesen
systemctl reload dienst.service
# Dienst aktivieren
systemctl enable dienst.service
# Dienst deaktivieren
systemctl disable dienst.service
# Unit-Datei anzeigen:
systemctl cat dienst.service
```
##### Abhängikeiten von Diensten
```bash
# Abhängingkeiten anzeigen
systemctl list-dependencies
# Abhängikeiten eines bestimmten Dienstes anzeigen
systemclt list-dependencies dienst.service
```
##### Dienste ändern

Systemd-Dienste sollte man nicht durch Editieren der Orginaldatei verändern, 
sondern ein Kopie im Verzeichnis /etc/systemd/system anlegen und diese editieren.
Orginal-Dienste liegen in der Regel unter `/var/lib/systemd/system`.
Konfigurationen von Diensten (mit gleichem Namen) werden von Diensten in diesem Verzeichnis überschrieben.
Um z. B. zusätzliche Umgebungsvariablen an einen Dienst zu übergeben, kann auch ein Verzeichnis
`/etc/systemd/system/dienst.service.d` angelegt werden und dort eine Datei mit der Endung .conf anglegt werden,
in der dann zusätzliche Variablen an den Dienst übergeben werden z. B. `ENVIRONMENT="HTTP_PROXY=http://proxy:8080"`.

Änderungen von Diensten müssen systemd durch den Befehl `systemctl daemon-reload` mitgeteilt werden.

##### Eigenen Dienst erstellen

```bash
# Root-Shell
sudo -i
# Dienst-Konfigruationsdatei anlegen/editieren
vim /etc/systemd/system/meindienst.service
[Unit]
Description=Mein Dienst

[Service]
Type=simple
ExecStart=/usr/bin/meindienst.sh

[Install]
WantedBy=multi-user.target
```

##### Targets (Systemziele bzw. Systemzustände)

SysV Runlevel | 	systemd Target                                    | Bemerkung
--------------|-------------------------------------------------------|-------------------------------------------------------------------
0 	          | runlevel0.target, poweroff.target                     |	Herunterfahren des Systems
1, s, single  | runlevel1.target, rescue.target 	                  | Einzelbenutzermodus ohne Netzwerk
2, 4 	      | runlevel2.target, runlevel4.target, multi-user.target |	Benutezrdefinierte Runlevel, per Default: identisch mit Runlevel 3
3 	          | runlevel3.target, multi-user.target                   | Mehrbenutermodus mit Netzwerk ohne grafisches User Interface (GUI)
5 	          | runlevel5.target, graphical.target                    | Mehrbenutermodus mit Netzwerk und grafischem User Interface (GUI)
6 	          | runlevel6.target, reboot.target                       |	Neustart des Systems (Reboot)
emergency 	  | emergency.target 	                                  | Notfall/Rettungs-Shell 

Quelle: Arch Linux Wiki (siehe Links)

##### Standard Runlevel konfigurieren

```bash
# Standard Runlevel anzeigen
systemctl get-default
graphical.target
# Standard Runlevel auf 3 setzen
systemctl set-default multi-user.target
Created symlink /etc/systemd/system/default.target → /lib/systemd/system/multi-user.target.
# Standard Runlevel auf 5 setzen
systemctl set-default graphical.target
Removed /etc/systemd/system/default.target.
Created symlink /etc/systemd/system/default.target → /lib/systemd/system/graphical.target.
```
### Auszug weiterer Systemd Komponenten und Kommandos

- systemd-logind (loginctl)
- systemd-networkd (networkctl)
- systemd-timesyncd (timedatectl)
- systemd-journald (journalctl)

### Beispiele Journald

```bash
# Syslog ausgeben (beginnend mit ältestem Eintrag)
journalctl
# Syslog fortlaufend ausgeben
journalctl -f
# Syslog rückwärts ausgeben (beginnend mit neustem Eintrag)
journalctl -r
# Syslog für bestimmten Dienst (unit) ausgeben
journalctl -u dienst.service
# Syslog für bestimmten Dienst fortlaufend ausgeben
journalctl -f -u dienst.service
# Boot-Log anzeigen
journalclt --boot
```
Links:
- https://wiki.archlinux.org/title/Systemd
- https://wiki.ubuntuusers.de/systemd/
- https://wiki.ubuntuusers.de/systemd/Units/#Eigene-Units-anlegen
- https://de.wikipedia.org/wiki/Systemd

