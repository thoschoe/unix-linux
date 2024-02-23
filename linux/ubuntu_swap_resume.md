# Ubuntu - Warnmeldung bei Neuerstellung der intialen Ramdisk bzgl. SWAP

Bei Nachträglichen Änderungen der SWAP-Partition ist die Resume-Variable nicht gesetzt.
Dies führt beim Update des initramfs zu Warunungen.

Hinweise:
- Bei der OS-Installation wird dies durch den Installer erledigt.
- Bei Ubuntu 20 wird ein SWAP-File  auf der Filesystemroot (/swap.img) erstellt.
- Bei Ubuntu 22 ab Installer ISO 22.04.2 wird kein SWAP-File erstellt, wenn eine SWAP-Partion installiert wird.

### Behebung des Problems an einem Beispiel:

Warnmeldung bei update-initramfs:

```txt
update-initramfs: Generating /boot/initrd.img-5.4.0-66-generic
I: The initramfs will attempt to resume from /dev/sdd1
I: (UUID=eec4be31-a2b4-31bf-7e09-e34507a8eb26)
I: Set the RESUME variable to override this.
```

```bash
# Blockdevice ID anzeigen:
blkid | grep swap
/dev/sdd1: UUID="eec4be31-a2b4-31bf-7e09-e34507a8eb26" TYPE="swap" PARTUUID="7ae5d632-2b38-1b34-8556-0f37ced7cd6a"

# Blockdevice ID der SWAP-Partition anzeigen:
blkid | awk -F\" '/swap/ {print $2}'
eec4be31-a2b4-31bf-7e09-e34507a8eb26

# Text für Konfigdatei für initramfs zusammenstellen:
printf "RESUME=UUID=$(blkid | awk -F\" '/swap/ {print $2}')\n"
RESUME=UUID=eec4be31-a2b4-31bf-7e09-e34507a8eb26
```
### Befehl für das Setzten der RESUME-Variable für intitramfs + Ausgabe auf der Konsole

```bash
printf "RESUME=UUID=$(blkid | awk -F\" '/swap/ {print $2}')\n" | tee /etc/initramfs-tools/conf.d/resume
RESUME=UUID=eec4be31-a2b4-31bf-7e09-e34507a8eb26

# Anzeige der Konfigdatei
cat /etc/initramfs-tools/conf.d/resume
RESUME=UUID=eec4be31-a2b4-31bf-7e09-e34507a8eb26

# Initiale Ramdisk fuer alle Kernel unter /boot neu erstellen
# Die Warnmeldung sollte dabei nicht mehr kommen
update-initramfs -u -k all
```

Wikipedia-Link zu Initramfs:  
https://de.wikipedia.org/wiki/Initramfs

