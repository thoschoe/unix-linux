# Linux - Informationen zur Hardware anzeigen

```bash
# Infos zur Hardware anzeigen
lshw
# Kurzinfos zur Hardware anzeigen
lshw -short

# Infos zur CPU anzeigen lassen
lscpu
# und auch
cat /proc/cpuinfo

# Infos zu PCI Geraeten anzeigen lassen
lspci

# Infos zu USB Geraeten anzeigen lassen
lsusb

# Infos zu Speicher anzeigen lassen
lsmem
# und auch
cat /proc/meminfo

# Infos zur GPU anzeigen lassen
lsgpu

# Infos zu Block-Devices (Festplatten) anzeigen lassen
lsblk

# Infos zum Netzwerk anzeigen
nmcli
# und auch
ethtool # muss ggf. installiert werden
# und auch
ifconfig
```


