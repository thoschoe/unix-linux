# Proxy-Server verwenden

### Proxy-Server für die Shell

```bash
# Proxy-Variablen temporär setzten:
export http_proxy="http://proxy:3128"
export https_proxy="http://proxy:3128"
export no_proxy="meinnetz.lan"
```
Soll die Proxy-Konfiguration dauerhaft erfolgen, können die Shell-Variablen in entsprechenden Konfigurationsdateien gesetzt werden:

##### Ubuntu/Debian
/etc/environment

##### SuSE
/etc/default/proxy

##### Weitere Möglichkeiten
/etc/profile  
/etc/bash_rc

### Proxy Server für apt

##### bis Ubuntu 14.04 (ohne systemd)
- Editieren der Datei /etc/apt/apt.conf
```yaml
Acquire::http::Proxy "http://proxyserver:3128;
Acquire::https::Proxy "http://proxyserver:3128;
```
##### ab Ubuntu 16.04 (mit systemd)
- Anlegen/Editieren der Datei /etc/apt/apt.conf.d/90curtin-aptproxy
```yaml
Acquire::http::Proxy "http://proxyserver:3128;
Acquire::https::Proxy "http://proxyserver:3128;
```

### Proxy Server für snapd
- Anlegen/Editieren der Datei /etc/systemd/system/snapd.service.d/snap_proxy.conf
```bash
# Verzeichnis snapd.service.d anlegen
mkdir -p /etc/systemd/system/snapd.service.d
# Datei snap_proxy.conf editieren
vim /etc/systemd/system/snapd.service.d/snap_proxy.conf
Environment="HTTP_PROXY=http://proxyserver:3128"
Environment="HTTPS_PROXY=http://proxyserver:3128"
```
