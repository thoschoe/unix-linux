# Ubuntu - Lokale Firewall UFW

uwf bedeutet "uncomplicated firewall"

### Verhalten einstellen

```bash
# Root-Shell
sudo -i

# Alles erlauben, was nicht explizit verboten wird
ufw default allow

# Alles verbieten, was nicht explizit erlaubt wird
ufw default deny

# Alles ablehnen, was nicht explizit erlaubt wird
ufw defaul reject
```
Beispiele

```bash
# HTTP-Zugriff auf Webserver erlauben
ufw allow http
# oder auch feingranularer
ufw allow from 192.168..0.1/24 proto tcp port 80

# SSH-Zugriff erlauben
ufw allow ssh
```

### Firewall Ein-/Ausschalten

```bash
# Aktivieren
ufw enable
# Deaktivieren
ufw disable
```
Link:  
https://wiki.ubuntuusers.de/ufw/