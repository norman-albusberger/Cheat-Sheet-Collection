# Apple Mac Terminal Cheat Sheet

## Grundlegende Befehle
```sh
ls        # Verzeichnisinhalt auflisten
cd        # Verzeichnis wechseln
pwd       # Aktuelles Verzeichnis anzeigen
mkdir     # Neues Verzeichnis erstellen
rm        # Datei löschen
rm -r     # Verzeichnis und Inhalt löschen
touch     # Neue Datei erstellen
cp        # Datei kopieren
mv        # Datei verschieben oder umbenennen
```

## Dateisystem und Navigation
```sh
ls -la         # Alle Dateien inkl. versteckter anzeigen
tree           # Verzeichnisbaum anzeigen (evtl. nachinstallieren: brew install tree)
find . -name "*.txt"  # Dateien suchen
```

## Datei- und Verzeichnisberechtigungen
```sh
chmod 755 Datei   # Zugriffsrechte ändern
chown user Datei  # Besitzer ändern
chgrp gruppe Datei # Gruppenzugehörigkeit ändern
```

## Prozesse und Systeminformationen
```sh
ps aux      # Laufende Prozesse anzeigen
top         # Live-Prozessüberwachung
kill PID    # Prozess beenden
kill -9 PID # Prozess sofort beenden
htop        # Erweiterte Prozessanzeige (evtl. nachinstallieren: brew install htop)
```

## Netzwerkbefehle
```sh
ping google.com        # Netzwerkverbindung testen
ifconfig              # Netzwerkkonfiguration anzeigen
netstat -rn          # Routing-Tabelle anzeigen
nslookup domain.com  # DNS-Abfrage
traceroute google.com # Verbindungswege anzeigen (evtl. nachinstallieren: brew install inetutils)
nmap -sn 192.168.1.0/24  # Alle Geräte im Netzwerk scannen (evtl. nachinstallieren: brew install nmap)
nmap -p 1-65535 192.168.1.1  # Offene Ports auf einem bestimmten Host scannen
arp -a               # Netzwerkgeräte über ARP-Tabelle anzeigen
```

## Paketverwaltung mit Homebrew
```sh
brew install paket  # Paket installieren
brew uninstall paket  # Paket deinstallieren
brew update         # Homebrew aktualisieren
brew upgrade        # Installierte Pakete aktualisieren
```

## Shell- und Terminal-Shortcuts
```sh
CTRL + C  # Prozess abbrechen
CTRL + D  # Terminal beenden
CTRL + A  # Zum Anfang der Zeile springen
CTRL + E  # Zum Ende der Zeile springen
CTRL + U  # Zeile löschen
CTRL + L  # Terminal bereinigen
```

## macOS-spezifische Befehle
```sh
open .              # Finder im aktuellen Verzeichnis öffnen
open file.txt       # Datei mit Standardanwendung öffnen
defaults write com.apple.finder AppleShowAllFiles -bool true; killall Finder  # Versteckte Dateien einblenden
defaults write com.apple.finder AppleShowAllFiles -bool false; killall Finder # Versteckte Dateien ausblenden
```

## SSH & Remote-Verbindungen
```sh
ssh user@host       # Mit Server verbinden
scp datei user@host:/pfad  # Datei auf Server kopieren
rsync -avz quelle ziel  # Dateien synchronisieren
```

## Weitere nützliche Befehle
```sh
history            # Letzte Befehle anzeigen
alias ll='ls -la' # Alias setzen
clear             # Terminal aufräumen
df -h             # Speicherplatz anzeigen
du -sh *          # Größe von Dateien/Verzeichnissen anzeigen
```

## Terminal-Profilerstellung (.zshrc / .bashrc)
```sh
echo "export PATH=\"$HOME/bin:$PATH\"" >> ~/.zshrc  # Pfadvariable anpassen
source ~/.zshrc   # Änderungen aktivieren
```

Viel Spaß mit deinem Mac Terminal! 🚀
