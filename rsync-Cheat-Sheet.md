# Rsync Cheat Sheet

## Einführung
`rsync` ist ein leistungsstarkes Tool zum Kopieren und Synchronisieren von Dateien und Verzeichnissen, sowohl lokal als auch über Netzwerke. Es unterstützt inkrementelle Übertragungen, Komprimierung und viele erweiterte Optionen.

## Grundlegende Syntax
```sh
rsync [OPTIONEN] QUELLE ZIEL
```

## Grundlegende Nutzung
```sh
rsync -av quelle/ ziel/  # Kopiert den Inhalt von 'quelle' nach 'ziel' (mit Erhaltung von Berechtigungen)
rsync -av quelle ziel/    # Kopiert das Verzeichnis 'quelle' als Ganzes in 'ziel'
rsync -av quelle ziel     # Kopiert und benennt 'quelle' in 'ziel' um
rsync -av quelle/ user@remote:/pfad/  # Dateien zu einem entfernten Server kopieren
```

## Häufige Optionen
```sh
-a  # Archivmodus (rekursiv, Rechte, Zeitstempel, Symlinks, Geräte)
-v  # Ausführlicher Modus
-z  # Daten während der Übertragung komprimieren
-P  # Fortschrittsanzeige + Fortsetzen unterbrochener Übertragungen
--delete  # Löscht Dateien am Ziel, die in der Quelle nicht mehr existieren
--exclude='*.log'  # Ausschließen bestimmter Dateien oder Verzeichnisse
--dry-run  # Testlauf ohne tatsächliche Änderungen
```

## Lokale Synchronisation
```sh
rsync -av /home/user/Dokumente/ /backup/Dokumente/  # Backup erstellen
rsync -av --delete /projekte/ /backup/projekte/    # 1:1 Kopie mit Löschung von nicht vorhandenen Dateien
```

## Remote Synchronisation
```sh
rsync -av /home/user/Dokumente/ user@server:/backup/Dokumente/  # Hochladen auf einen Server
rsync -av user@server:/backup/Dokumente/ /home/user/Dokumente/  # Herunterladen vom Server
rsync -av -e ssh /home/user/Dokumente/ user@server:/backup/  # SSH für sichere Übertragung
```

## Synchronisation mit Bandbreitenbegrenzung
```sh
rsync -av --bwlimit=5000 quelle/ ziel/  # Begrenzung auf 5 MB/s
```

## Inkrementelle Backups mit Hardlinks
```sh
rsync -av --link-dest=/backup/backup_alt /quelle/ /backup/backup_neu/  # Speicherplatzsparendes Backup
```

## Synchronisation mit Datei- und Verzeichnisausschlüssen
```sh
rsync -av --exclude='*.tmp' --exclude='cache/' quelle/ ziel/  # Exkludiert temporäre Dateien und Cache-Ordner
rsync -av --exclude-from='exclude-list.txt' quelle/ ziel/  # Ausschlüsse aus einer Datei laden
```

## Fortschrittsanzeige & Logging
```sh
rsync -av --progress quelle/ ziel/  # Fortschritt jeder Datei anzeigen
rsync -av --log-file=rsync.log quelle/ ziel/  # Protokoll schreiben
```

## Fortsetzen unterbrochener Übertragungen
```sh
rsync -avP quelle/ ziel/  # Fortsetzt unterbrochener Kopiervorgänge
rsync -av --append quelle/ ziel/  # Fortsetzt, wenn teilweise übertragene Dateien existieren
```

## Parallele Übertragung mehrerer Dateien
```sh
rsync -av --info=progress2 quelle/ ziel/  # Zeigt eine detaillierte Fortschrittsanzeige
```

## Sicheres Backup über SSH mit rsync
```sh
rsync -av -e "ssh -p 2222" /quelle/ user@remote:/ziel/  # SSH mit Port 2222
rsync -av --rsync-path="sudo rsync" /quelle/ user@remote:/ziel/  # Rsync mit sudo auf dem Zielhost
```

## Löschen von nicht mehr vorhandenen Dateien im Zielverzeichnis
```sh
rsync -av --delete quelle/ ziel/  # Löscht Dateien im Ziel, die in der Quelle nicht mehr existieren
```

## Rsync über einen Tunnel
```sh
ssh -L 9000:remote-host:22 user@remote-host  # SSH-Tunnel öffnen
rsync -av -e "ssh -p 9000" /lokal/ localhost:/remote/  # Rsync über den Tunnel
```

## Backup mit Zeitstempel
```sh
rsync -av /quelle/ /backup/$(date +"%Y-%m-%d")/  # Erstellt tägliche Backups mit Datum im Namen
```
