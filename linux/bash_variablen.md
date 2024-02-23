# Linux Variablen in der Shell (BASH)

Variablen werden mit "$" angesprochen, ggf. sind auch geschweifte Klammern zu verwenden.

$0 - Dateiname

$? - Rückgabewert des zuletzt ausgeführten Programms oder Befehls (0=OK)

$PATH - Pfade in denen Programme gesucht werden  
Die PATH-Variable wird von links nach rechts ausgewertet, d. h. der erste Treffer wird ausgefuehrt.  
BSP: Gleichnamige Programme in /usr/local/bin werden in der Regel vor Programmen in /usr/bin ausgeführt.

PATH-Variable anzeigen:

```bash
echo $PATH
# oder auch
echo ${PATH}
usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/snap/bin
```
Bei den meisten Linux-Systemen wird diese in der Datei /etc/environment gesetzt.
In einigen Systemen wird sie in der Datei /etc/profile gesetzt.

### Strings in Variablen beschneiden

Man kann in Variablen mit "#" von link und mit "%" von rechts beschneiden.

Beispiel:

```bash
# Textdateien einzeln auflisten
ls *.txt
datei1.txt  datei2.txt  datei3.txt

# Dateinamen von Textdatein in einem Verzeichnis ohne Endung .txt ausgeben
# Alles nach dem ersten Punkt von rechts wird von der Variable "$i" abgeschnitten.
# Waeren mehrere Punkte vorhanden und soll alles nach dem ersten Punkt abgeschnitten werden,
# muesste das Prozentzeichnen doppelt verwendet werden: ${i%%.*}
for i in `ls *.txt`; do echo ${i%.*}; done
datei1
datei2
datei3

# TXT-Dateien in md-Dateien umbenennen
for i in `ls *.txt`; do mv $i ${i%.*}.md; done
# Auflisten
ls
datei1.md  datei2.md  datei3.md
```