# Ubuntu - DNS-Cache bereinigen

 - - -

Hinweis:  
Bei Ubuntu 18 funktioniert nur der Befehl "systemd-resolve".  
Bei Ubuntu 20 funktionieren sowohl "systemd-resolve" als auch "resolvectl".  
Ab Ubuntu 22 funktioniert nur noch den Befehl "resolvectl".

### Ubuntu 18-20:

```bash
# Root-Shell
sudo -i

# DNS-Statistik anzeigen:
systemd-resolve --statistics

# Auszug der Ausgabe zu Cache:
# ...
# Cache
#  Current Cache Size: 2
#          Cache Hits: 28
#        Cache Misses: 142
# ...

# DNS-Cache löschen
systemd-resolve --flush-caches

# Status anzeigen:
systemd-resolve --status
```

### Ubuntu 20-22

```bash
# Root-Shell
sudo -i

# DNS-Statistik anzeigen:
resolvectl statistics

# Auszug der Ausgabe zu Cache:
# ...
# Cache
#   Current Cache Size: 5
#           Cache Hits: 6632
#         Cache Misses: 7475

# DNS-Cache löschen
resolvectl flush-caches

# Status anzeigen:
resolvectl status
```