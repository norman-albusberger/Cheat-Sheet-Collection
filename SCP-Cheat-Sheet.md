# SCP Cheat Sheet

## Einführung
`scp` (Secure Copy Protocol) ist ein Befehl zum sicheren Kopieren von Dateien zwischen lokalen und entfernten Hosts über SSH.

## Grundlegende Syntax
```sh
scp [OPTIONEN] QUELLE ZIEL
```

## Grundlegende Nutzung
```sh
scp datei.txt user@remote:/ziel/pfad/  # Einzelne Datei auf einen Server kopieren
scp user@remote:/pfad/datei.txt /lokaler/pfad/  # Datei vom Server herunterladen
scp -r ordner/ user@remote:/ziel/pfad/  # Ein ganzes Verzeichnis rekursiv kopieren
```

## Häufige Optionen
```sh
-P 2222  # Alternativen SSH-Port angeben
-i key.pem  # SSH-Schlüssel zur Authentifizierung verwenden
-r  # Rekursives Kopieren von Verzeichnissen
-v  # Verbose-Modus (detaillierte Ausgabe)
-C  # Komprimierung während der Übertragung
-l 500  # Bandbreitenbegrenzung in Kbit/s
```

## Dateien auf einen Remote-Server kopieren
```sh
scp datei.txt user@remote:/home/user/  # Datei ins Home-Verzeichnis des Users kopieren
scp -r /lokaler/ordner user@remote:/backup/  # Verzeichnis auf den Server kopieren
scp -P 2222 datei.txt user@remote:/ziel/  # Verbindung über einen alternativen SSH-Port
```

## Dateien von einem Remote-Server herunterladen
```sh
scp user@remote:/pfad/datei.txt /lokaler/pfad/  # Datei vom Server auf den lokalen Rechner holen
scp -r user@remote:/backup/ /lokales/backup/  # Verzeichnis rekursiv herunterladen
scp -P 2222 user@remote:/logfiles/*.log /lokaler/pfad/  # Alle Log-Dateien herunterladen
```

## SCP mit SSH-Schlüssel (Zertifikatsauthentifizierung)
```sh
scp -i ~/.ssh/id_rsa datei.txt user@remote:/ziel/pfad/  # Authentifizierung mit privatem SSH-Schlüssel
scp -i ~/.ssh/mykey.pem user@remote:/pfad/datei.txt /lokaler/pfad/  # Zertifikatsbasierte Authentifizierung
```

## SCP über einen SSH-Tunnel
```sh
ssh -L 9000:remote-host:22 user@remote-host  # SSH-Tunnel erstellen
scp -P 9000 datei.txt user@localhost:/ziel/pfad/  # Datei über den Tunnel kopieren
```

## Parallele Dateiübertragungen mit `scp` über `tar` und `ssh`
```sh
tar -cf - quelle/ | ssh user@remote 'tar -xf - -C /ziel/pfad/'  # Mehrere Dateien effizient übertragen
```

## Sicheres Kopieren mit Log- und Fortschrittsanzeige
```sh
scp -v datei.txt user@remote:/ziel/pfad/  # Verbose-Modus für Debugging
rsync -av --progress -e ssh datei.txt user@remote:/ziel/pfad/  # Alternative mit Fortschrittsanzeige
```

