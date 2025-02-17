# Ubuntu Cheat-Sheet: Wichtige Konsolenbefehle

## 🔹 System-Informationen
| Befehl | Beschreibung | Optionen |
|--------|-------------|----------|
| `lsb_release -a` | System-Version anzeigen | - |
| `uname -r` | Kernel-Version anzeigen | - |
| `lscpu` | CPU-Details anzeigen | - |
| `free -h` | RAM-Nutzung anzeigen | -h (menschenlesbar) |
| `df -h` | Festplattenspeicher anzeigen | -h (menschenlesbar) |

## 🔹 Systemd-Prozess-Management
| Befehl | Beschreibung | Optionen |
|--------|-------------|----------|
| `sudo systemctl start dienstname` | Dienst starten | - |
| `sudo systemctl stop dienstname` | Dienst beenden | - |
| `sudo systemctl restart dienstname` | Dienst neu starten | - |
| `sudo systemctl status dienstname` | Status eines Dienstes anzeigen | - |
| `sudo systemctl enable dienstname` | Dienst beim Booten starten | - |
| `sudo systemctl disable dienstname` | Dienst vom Autostart entfernen | - |
| `sudo systemctl list-units --type=service` | Alle aktiven Dienste anzeigen | --all (alle Dienste anzeigen) |
| `sudo journalctl -u dienstname` | Logs eines Dienstes anzeigen | -f (Live-Log) |

## 🔹 Benutzer- und Rechteverwaltung
| Befehl | Beschreibung | Optionen |
|--------|-------------|----------|
| `whoami` | Aktuellen Benutzer anzeigen | - |
| `su - username` | Benutzer wechseln | - |
| `sudo adduser username` | Neuen Benutzer anlegen | - |
| `sudo usermod -aG groupname username` | Benutzer zu einer Gruppe hinzufügen | -a (append), -G (Gruppe) |
| `groups username` | Alle Gruppen eines Benutzers anzeigen | - |
| `chmod 755 datei.txt` | Besitzer kann alles, andere nur lesen/ausführen | -R (rekursiv) |
| `chown user:group datei.txt` | Eigentümer ändern | -R (rekursiv) |

### Gruppen- und Benutzer-Berechtigungen (chmod)
| Modus  | Bedeutung | Beispiel |
|--------|-----------|----------|
| 7 (rwx) | Lesen, Schreiben, Ausführen | `chmod 777 datei.txt` |
| 6 (rw-) | Lesen, Schreiben | `chmod 664 datei.txt` |
| 5 (r-x) | Lesen, Ausführen | `chmod 555 script.sh` |
| 4 (r--) | Nur Lesen | `chmod 444 dokument.txt` |
| 3 (-wx) | Schreiben, Ausführen | `chmod 311 script.sh` |
| 2 (-w-) | Nur Schreiben | `chmod 222 tmpfile` |
| 1 (--x) | Nur Ausführen | `chmod 111 executable.sh` |
| 0 (---) | Keine Rechte | `chmod 000 geheime_datei.txt` |

## 🔹 Netzwerkbefehle & Scans
| Befehl | Beschreibung | Optionen |
|--------|-------------|----------|
| `ip a` | IP-Adresse anzeigen | - |
| `ping 8.8.8.8` | Netzwerkverbindung testen | -c [X] (Anzahl der Pings) |
| `netstat -tulnp` | Offene Ports anzeigen | -t (TCP), -u (UDP), -l (listening), -n (numerisch), -p (Prozess) |
| `ss -tulnp` | Alle Netzwerkverbindungen anzeigen | - |
| `nmap -F 192.168.1.1` | Schneller Netzwerkscan | -p [1-65535] (alle Ports scannen) |
| `sudo tcpdump -i eth0` | Netzwerkverkehr in Echtzeit überwachen | -X (Hex + ASCII), -vv (sehr ausführlich) |

### DNS-Management
| Befehl | Beschreibung | Optionen |
|--------|-------------|----------|
| `nslookup domain.com` | DNS-Auflösung prüfen | - |
| `dig domain.com` | Detaillierte DNS-Informationen anzeigen | +short (nur die IP anzeigen) |
| `host domain.com` | Einfache DNS-Abfrage durchführen | - |

### Firewall-Management (UFW)
| Befehl | Beschreibung | Optionen |
|--------|-------------|----------|
| `sudo ufw status` | Status der Firewall anzeigen | - |
| `sudo ufw enable` | Firewall aktivieren | - |
| `sudo ufw disable` | Firewall deaktivieren | - |
| `sudo ufw allow 22/tcp` | Port 22 (SSH) erlauben | - |
| `sudo ufw deny 80/tcp` | Port 80 (HTTP) blockieren | - |
| `sudo ufw delete allow 22/tcp` | Regel entfernen | - |

### SCP: Datei-Transfer zwischen Servern
| Befehl | Beschreibung | Optionen |
|--------|-------------|----------|
| `scp datei user@server:/pfad` | Datei zu einem Server kopieren | -r (rekursiv für Verzeichnisse) |
| `scp user@server:/pfad/datei .` | Datei von einem Server herunterladen | - |
| `scp -P 2222 datei user@server:/pfad` | Port für SCP ändern | -P (Portnummer angeben) |


## 🔹 Arbeiten mit Pipes (`|`)

Das Pipe-Symbol (`|`) leitet die Ausgabe eines Befehls als Eingabe an einen anderen Befehl weiter.

### Beispiele:

| Befehl                | Beschreibung                                     |
| --------------------- | ---------------------------------------------- |
| `ls -lah | grep '.txt'`     | Zeigt nur `.txt`-Dateien aus der `ls`-Liste |
| `ps aux | grep firefox`     | Sucht den Prozess `firefox` in der Liste aller Prozesse |
| `cat datei.txt | wc -l`     | Zählt die Zeilen in einer Datei |
| `df -h | grep '/dev/sda1'`  | Zeigt den Speicherplatz für `/dev/sda1` |
| `cat /var/log/syslog | less` | Ermöglicht das Scrollen durch die System-Logs |




## Nützliche Tools
| Tool | Beschreibung |
|------|-------------|
| `htop` | Erweiterte Prozessverwaltung mit interaktiver Ansicht |
| `tmux` | Terminal-Multiplexer für Sitzungsverwaltung |
| `ncdu` | Detaillierte Analyse der Festplattennutzung |
| `rsync` | Leistungsstarker Datei-Synchronisationsbefehl |
| `jq` | JSON-Daten einfach in der Konsole formatieren |
| `aircrack-ng` | Tool zur Analyse und zum Testen von WLAN-Sicherheiten |
| `john` | John the Ripper, ein Passwort-Cracking-Tool |
| `metasploit` | Exploitation-Framework für Sicherheitstests |
| `hydra` | Schnelles Passwort-Cracking-Tool für verschiedene Protokolle |
| `sqlmap` | Automatisches SQL-Injection-Tool zur Sicherheitsanalyse |
| `nikto` | Webserver-Sicherheitsprüfungstool |


