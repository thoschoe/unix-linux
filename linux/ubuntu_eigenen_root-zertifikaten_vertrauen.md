# Ubuntu - Eigenen Root-Zertifikaten vertrauen

Hat man im Unternehmen eigene Root-Zertifikate, soll diesen ggf. auch auf auf der Shell vertraut werden.

Dafür gibt es 2 Möglichkeiten:

Hinweis: Die Zertifikatsdateien müssen im PEM-Format vorliegen und die Dateiendung .crt haben.

1. Interaktiv:
```bash
# Root-Shell
sudo -i
# Zertfikat kopieren
cp eigenes-root-zertifikat.crt /usr/share/ca-certificates
# Zertifikats-Truststore neu konfiguerien
dpkg-reconfigure ca-certificates
Neuen Zertifikaten von Zertifizierungsstellen vertrauen?
Ja
Zu aktivierende Zertifikate:
[*] eigenes-root-zertifikat.crt

Updating certificates in /etc/ssl/certs...

# Zertfifikat anzeigen lassen
ls -l /etc/ssl/certs/ | grep eigenes-root-zertifikat
```
Diese Methode:
- Erstellt einen Link für die Zertifikatsdatei in /etc/ssl/certs:
  eigenes-root-zertifikat.pem -> /usr/share/ca-certificates/eigenes-root-zertifikat.crt
- Erstellt einen Link auf den Link der Zertifikatsdatei:
  abe0e41d.0 -> eigenes-root-zertifikat.pem
- Fügt das Zertifikat an Zertifikatsdatei an, welche alle Trust-Zertifikate enthält:
  /etc/ssl/certs/ca-certificates.crt

2. Bereitstellung ohne Interaktion:

```bash
# Root-Shell
sudo -i
# Zertfikat kopieren
cp eigenes-root-zertifikat.crt /usr/local/share/ca-certificates
# Trusstore neu erstellen
update-ca-certificates

# Zertfifikat anzeigen lassen
ls -l /etc/ssl/certs/ | grep eigenes-root-zertifikat
```
Diese Methode: 
- Erstellt einen Link für die Zertifikatsdatei:
  eigenes-root-zertifikat.pem -> /usr/local/share/ca-certificates/eigenes-root-zertifikat.crt
  Erstellt einen Link auf den Link der Zertifikatsdatei:
  abe0e41d.0 -> eigenes-root-zertifikat.pem
- Fügt das Zertifikat an Zertifikatsdatei an, welche alle Trust-Zertifikate enthält:
  /etc/ssl/certs/ca-certificates.crt

Hinweis:  
Bei der 2. Methode wird das Zertifikat nicht bei `dpkg-reconfigure ca-certificates` im Menue angezeigt.

