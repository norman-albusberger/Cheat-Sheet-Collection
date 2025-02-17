# Hacker-Guide: Grundlagen und Werkzeuge für Ethical Hacking

## 🔹 Einführung
Hacking bezieht sich auf das Analysieren und Manipulieren von Computersystemen, Netzwerken und Anwendungen. Ethical Hacking wird für Sicherheitsanalysen und Penetrationstests genutzt, um Schwachstellen aufzudecken und Systeme zu schützen.

## 🔹 Grundlagen des Hackings
### 1. Hacking-Kategorien
- **White-Hat**: Sicherheitsexperten, die Systeme schützen
- **Black-Hat**: Kriminelle Hacker mit böswilliger Absicht
- **Grey-Hat**: Hacken aus Neugierde oder zur Aufdeckung von Schwachstellen ohne Genehmigung

### 2. Phasen eines Penetrationstests
1. **Reconnaissance** – Informationsbeschaffung
2. **Scanning** – Netzwerkscans und Schwachstellenanalyse
3. **Exploitation** – Angriffe und Sicherheitslücken ausnutzen
4. **Privilege Escalation** – Höhere Berechtigungen erlangen
5. **Maintaining Access** – Persistenz im System bewahren
6. **Covering Tracks** – Spuren verwischen

## 🔹 Wichtige Hacking-Tools mit Beispielen
### 1. Netzwerkanalyse & Scanning
- **nmap** – Netzwerk-Scanning und Port-Analyse
  ```bash
  nmap -A -T4 example.com  # Detaillierte Netzwerkanalyse mit OS-Erkennung
  ```
- **wireshark** – Netzwerkanalyse und Traffic-Überwachung
  ```bash
  sudo wireshark  # Startet die Wireshark-GUI
  ```
- **masscan** – Hochgeschwindigkeits-Scanning großer Netzwerke
  ```bash
  sudo masscan -p80,443,22 --rate=1000 192.168.1.0/24
  ```

### 2. Schwachstellenanalyse & Exploitation
- **metasploit** – Framework für Exploits und Penetrationstests
  ```bash
  msfconsole  # Startet Metasploit
  use exploit/multi/http/struts_dmi_exec  # Wählt ein Exploit
  ```
- **sqlmap** – Automatisierte SQL-Injection-Tests
  ```bash
  sqlmap -u "http://example.com/page?id=1" --dbs  # Findet Datenbanken
  ```
- **john** (John the Ripper) – Passwort-Cracking
  ```bash
  john --wordlist=passwords.txt hashes.txt  # Cracken von Passwort-Hashes
  ```
- **hydra** – Brute-Force-Angriffe auf Logins
  ```bash
  hydra -L users.txt -P pass.txt ssh://target.com  # SSH Brute-Force
  ```

### 3. Web-Hacking & Sniffing
- **burpsuite** – Proxy zum Analysieren und Manipulieren von HTTP/S Traffic
  ```bash
  burpsuite  # Startet die BurpSuite GUI
  ```
- **nikto** – Scanner für Webserver-Schwachstellen
  ```bash
  nikto -h http://example.com  # Scannt eine Website nach Schwachstellen
  ```
- **mitmproxy** – Man-in-the-Middle-Angriffe und Traffic-Analyse
  ```bash
  mitmproxy -p 8080  # Startet den Proxy auf Port 8080
  ```

### 4. WLAN-Hacking & Sniffing
- **aircrack-ng** – WLAN-Sicherheitsanalyse
  ```bash
  airmon-ng start wlan0  # Setzt WLAN-Adapter in Monitor-Modus
  airodump-ng wlan0mon  # Snifft WLAN-Verkehr
  ```
- **reaver** – Brute-Force-WPS-PIN-Angriffe
  ```bash
  reaver -i wlan0mon -b XX:XX:XX:XX:XX:XX -vv
  ```
- **kismet** – WLAN-Passives Scanning
  ```bash
  kismet -c wlan0  # Startet Kismet auf WLAN-Interface
  ```

### 5. Reverse Engineering & Malware-Analyse
- **radare2** – Open-Source Reverse Engineering Framework
  ```bash
  r2 -A malware.exe  # Analysiert eine ausführbare Datei
  ```
- **ghidra** – Disassembler für Malware-Analyse
  ```bash
  ./ghidraRun  # Startet die Ghidra-GUI
  ```
- **volatility** – Forensische Speicheranalyse
  ```bash
  volatility -f memory.dump --profile=Win7SP1x64 pslist  # Listet Prozesse aus Speicherabbild
  ```

## 🔹 Anonymität & Sicherheit
### 1. VPN & Tor-Netzwerk
- **Tor** – Anonymes Browsing
  ```bash
  tor  # Startet den Tor-Dienst
  ```
- **VPN** – Verschlüsselte Verbindung für mehr Sicherheit
  ```bash
  openvpn --config myvpn.ovpn  # Verbindet mit einer VPN-Config
  ```

### 2. Tails OS & Whonix
- **Tails** – Live-OS für anonymes Arbeiten
- **Whonix** – Virtuelles System für Anonymität

