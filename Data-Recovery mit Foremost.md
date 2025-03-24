# 🧰 Datenrettung mit `foremost` auf macOS (ARM/M1/M2/M3)

## 📦 Installation von Foremost

Stelle sicher, dass du **nicht im Rosetta-Terminal** arbeitest (also nativ im `arm64`-Modus):

```bash
arch
# Ausgabe muss sein: arm64
```

Falls nicht, öffne das Terminal über Spotlight (⌘ + Leertaste → "Terminal") und **entferne in den Informationen das Häkchen bei "Mit Rosetta öffnen"**.

### ➕ Foremost installieren

```bash
brew install foremost
```

> Homebrew installiert `foremost` standardmäßig in `/opt/homebrew/bin/foremost`

---

## 🔍 Schritt 1: Ziellaufwerk identifizieren

Finde heraus, welches Laufwerk deine Speicherkarte oder dein USB-Stick ist:

```bash
diskutil list
```

Beispielausgabe:

```
/dev/disk2 (external, physical):
   #:                       TYPE NAME                    SIZE       IDENTIFIER
   0:     FDisk_partition_scheme                        *16.0 GB    disk2
   1:             Windows_FAT_32 UNTITLED                16.0 GB    disk2s1
```

→ In diesem Fall wäre `disk2` das richtige Laufwerk.


## 🚀 Schritt 2: Daten wiederherstellen

Starte `foremost` mit folgendem Befehl:

```bash
sudo foremost -i /dev/disk2 -o ~/RecoveredFiles
```

- `-i`: Eingabedatei (dein Gerät – nicht die Partition, also z. B. `disk2`, **nicht** `disk2s1`)
- `-o`: Zielordner für die wiederhergestellten Dateien

> Du wirst nach deinem Passwort gefragt, da `foremost` Root-Rechte braucht.

### Was passiert genau?
1.	foremost liest das komplette Laufwerk (/dev/disk2) Sektor für Sektor.
2.	Es sucht nach Dateisignaturen (z. B. für JPEGs: FF D8 FF) und erkennt darüber den Beginn und das Ende von Dateien.
3.	Sobald eine Datei erkannt wird, wird sie sofort wiederhergestellt und in den Zielordner geschrieben.
4.	Du siehst währenddessen im Terminal Fortschrittsinformationen (Anzahl gefundener Dateien etc.).
 
Je nach Größe des Datenträgers und Dateitypen kann das mehrere Minuten bis Stunden dauern.

---

## 📁 Ergebnis ansehen

Nach dem Scan findest du deine Dateien im angegebenen Ausgabeordner:

```bash
open ~/RecoveredFiles
```

Dort liegen Unterordner wie `jpg`, `pdf`, `doc` etc. mit den geretteten Dateien.

---

## 🛠️ Optionale Parameter & Tipps

### 🔧 Nur bestimmte Dateitypen wiederherstellen

Mit `-t` kannst du gezielt Dateitypen angeben (z. B. nur JPEG und PDF):

```bash
sudo foremost -t jpg,pdf -i /dev/disk2 -o ~/RecoveredFiles
```

Unterstützte Typen (Auszug): `jpg`, `png`, `pdf`, `doc`, `xls`, `zip`, `avi`, `mp4`, `mp3`, `gif`, `txt`, `exe`, `ppt`, ...

---

### 🔧 Konfigurationsdatei nutzen (fortgeschritten)

Du kannst die Standard-Dateitypen oder eigene Formate in der Config-Datei anpassen:

```bash
sudo cp /opt/homebrew/etc/foremost.conf ~/foremost.conf
nano ~/foremost.conf
```

Dann verwendest du sie so:

```bash
sudo foremost -c ~/foremost.conf -i /dev/disk2 -o ~/RecoveredFiles
```

---

## 🧠 Tipps & Tricks

- **Immer erst im Lesezugriff arbeiten** – nie formatierte Medien beschreiben.
- **Wiederherstellungslaufwerk ≠ Quelllaufwerk!**
- **Lieber 2× scannen als unvollständig wiederherstellen.**
- Für große Speichermedien: Geduld mitbringen – der Vorgang kann mehrere Stunden dauern.
- Benutze ggf. einen USB-Kartenleser direkt, wenn SD-Karten über Adapter nicht zuverlässig erkannt werden.

---

## 🧹 Nach dem Scan

Wenn du fertig bist, kannst du die Speicherkarte wieder mounten oder auswerfen:

```bash
diskutil eject /dev/disk2
```

---

## ✅ Beispiel: Alles zusammen

```bash
diskutil list
diskutil unmountDisk /dev/disk2
sudo foremost -t jpg,pdf,doc -i /dev/disk2 -o ~/RecoveredFiles
open ~/RecoveredFiles
```

---

## 🕵️‍♂️ Forensik-Einsatz mit `foremost`

`foremost` wurde ursprünglich für den forensischen Einsatz entwickelt und eignet sich ideal zur Analyse von Rohdaten auf Speichermedien – selbst wenn das Dateisystem beschädigt ist.

### 🔍 Arbeiten mit Disk-Images

Anstatt direkt auf dem Originaldatenträger zu arbeiten, empfiehlt sich im forensischen Kontext das Erstellen eines Abbilds (z. B. `.img` oder `.dd`) und die anschließende Analyse dieses Images:

```bash
sudo dd if=/dev/disk2 of=~/Desktop/sdcard.img bs=4m
```

Dann:

```bash
sudo foremost -i ~/Desktop/sdcard.img -o ~/RecoveredFromImage
```

✅ So vermeidest du, versehentlich Daten auf dem Originaldatenträger zu verändern.

### 📁 Analyse von komprimierten und eingebetteten Formaten

`foremost` erkennt auch Daten, die sich innerhalb von:

- ZIP-Archiven
- Office-Dokumenten (z. B. `.docx`, `.xlsx`)
- PDF-Dateien

befinden, sofern sie durch klare Datei-Signaturen auffindbar sind.

### 🧰 Verwendung angepasster Signatur-Dateien

Im Forensik-Bereich ist es üblich, mit speziell angepassten `foremost.conf`-Dateien zu arbeiten, um z. B. auch proprietäre oder seltene Dateiformate zu erkennen.

Beispiel:

```conf
eml     y       2000000      From:             


```

### 📜 Logfiles für die Dokumentation

`foremost` erzeugt automatisch Logdateien, z. B.:

- `audit.txt`: Übersicht über alle gefundenen Dateien und Typen
- `foremost.log`: Detaillierte Informationen zur Analyse

Diese Logs sind nützlich für gerichtsfeste Dokumentationen und zur Nachvollziehbarkeit der Datenrettung.

---



## 📚 Weitere Infos

- Offizielle Webseite: [https://foremost.sourceforge.net/](https://foremost.sourceforge.net/)
