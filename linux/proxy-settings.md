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


### Proxy Server für snap
