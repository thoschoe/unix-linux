# Netzwerkanalyse-Tools

Portscanner nmap

```bash
# Installation
apt-get install nmap

# Portscan auf IP-Adresse (default 1-1024)
nmap 192.168.0.2

# Portscan auf SSH Port
nmap 192.168.0.2 -p 22
```

TCP Scanner tcpdump

```bash
# Installation
apt-get install tcpdump

# HTTP-Traffic scannen
tcpdump -n -A port 80
```

Datenverkehr anzeigen - iftop / nload

```bash
# Installation
apt-get install iftop
apt-get install nload
# Nutzung
ifotp
# Traffic auf bestimmten Interface
nload eth0
```

### Tools zur Bandbreitenmessung im lokalen Netz

- iperf - siehe: https://wiki.ubuntuusers.de/iperf/
- nttcp - siehe: https://wiki.ubuntuusers.de/nttcp/

### Graphisches Netzwerk-Analyse-Tool

Wireshark

Voraussetzung ist, dass eine graphische Oberflaeche vorhanden ist.

```bash
# Installation
apt-get install wireshark
```