# BASH Skripting - Bedingungen und Schleifen

### Beispiel IF-Bedingung

```bash
ls bla > /dev/null 2>&1
if [ $? < 0 ];
then
    echo "Fehler - Datei bla ist nicht vorhanden"
else
    echo "Datei bla ist vorhanden"
fi
```
- - -

### Beispiel FOR-Schleife

```bash
for var in `ls -1 *.zip`;
do
    ls -l $var;
    unzip $var;
done
```

- - -

### Beispiel WHILE-Schleife

```bash
while true;
do
    date;
    ping -c 2 server;
    echo "";
done
```

Links:  
- https://wiki.ubuntuusers.de/Shell/Bash-Skripting-Guide_f%C3%BCr_Anf%C3%A4nger/