

# 🔧 How‑To: Sonoff Zigbee Bridge Pro mit Tasmota und Zigbee-Koordinator flashen

Dieses Dokument beschreibt, wie man den **Sonoff Zigbee Bridge Pro** (ESP32 + CC2652P) mit **Tasmota** flasht und anschließend den **Zigbee-Koordinator** auf dem CC2652-Chip installiert.

---

## 📦 Voraussetzungen

- **Hardware**
  - Sonoff Zigbee Bridge Pro
  - USB‑TTL‑Adapter (3.3 V, z. B. CP2102 oder CH340)
  - Jumper‑Kabel oder gelötete Verbindung
  - Optional: Breadboard

- **Software**
  - `esptool.py` oder Flash‑Tool deiner Wahl
  - Tasmota Firmware:
    - `tasmota32-zbbrdgpro.factory.bin`
  - Zigbee-Koordinator Firmware:
    - `SonoffZBPro_coord_YYYYMMDD.hex` (z. B. 20220219)
  - Berry‑Skripte:
    - `intelhex.be`
    - `sonoff_zb_pro_flasher.be`
  - Optional: `Partition_Wizard.tapp` zum Erweitern des Dateisystems

> ⚠️ **Wichtig:** Verwende nur 3,3 V am TTL‑Adapter, **niemals 5 V**!

---

## 1️⃣ Gerät öffnen & Verdrahtung

1. Gummifüße abziehen, Schrauben lösen, Gehäuse vorsichtig öffnen.
2. Auf der Platine sind Pads mit `GND`, `GPIO00`, `RX`, `TX`, `3V3` beschriftet.
3. Verbinde die Pads mit dem USB‑TTL‑Adapter:

| Sonoff Pad | TTL‑Adapter |
|------------|------------|
| **GND**    | GND        |
| **GPIO00** | GND (nur während des Bootvorgangs!) |
| **RX**     | TX         |
| **TX**     | RX         |
| **3V3**    | 3.3 V      |

💡 **GPIO00 muss beim Einschalten mit GND verbunden sein**, damit der Bootloader startet.

---

## 2️⃣ Tasmota Firmware flashen

1. Lade die passende Firmware (`tasmota32-zbbrdgpro.factory.bin`) herunter.
2. Gerät in Flash‑Modus bringen (GPIO00 an GND halten und mit Strom versorgen).
3. Mit `esptool` flashen:

```bash
esptool.py --port <dein_port> write_flash 0x0 tasmota32-zbbrdgpro.factory.bin
```

4. Warten, bis der Flashvorgang abgeschlossen ist.
5. USB trennen, GPIO00 trennen, erneut starten.

---

## 3️⃣ WLAN konfigurieren & Template setzen

1. Nach dem Neustart verbindet sich das Gerät als **tasmota‑xxxx** Access Point.
2. Im Browser `192.168.4.1` aufrufen.
3. Eigenes WLAN (SSID + Passwort) eintragen und speichern.
4. Nach Verbindung ins Heimnetz per Browser aufrufen (IP im Router finden).
5. Unter **Configuration → Configure Other** Template setzen:

```json
{"NAME":"Sonoff Zigbee Pro","GPIO":[0,0,576,0,480,0,0,0,0,1,1,5792,0,0,0,3552,0,320,5793,3584,0,640,608,32,0,0,0,0,0,1,0,0,0,0,0,0],"FLAG":0,"BASE":1}
```

6. Speichern und Gerät neu starten.

---

## 4️⃣ Dateisystem & Berry-Skripte vorbereiten

1. Falls das Dateisystem zu klein ist → `Partition_Wizard.tapp` hochladen und ausführen.
2. Über **Manage File System** hochladen:
   - `intelhex.be`
   - `sonoff_zb_pro_flasher.be`
   - `SonoffZBPro_coord_YYYYMMDD.hex` (z. B. 20220219)

---

## 5️⃣ Zigbee-Koordinator flashen

1. In Tasmota-WebUI: **Consoles → Berry Scripting Console** öffnen.
2. Folgende Befehle ausführen:

```python
import sonoff_zb_pro_flasher as cc
cc.load("SonoffZBPro_coord_20220219.hex")
cc.check()
```

Erwartete Ausgabe:
```
FLH: Verification of HEX file OK
```

3. Dann flashen:
```python
cc.flash()
```

4. Vorgang dauert ca. 5 Minuten → Gerät nicht ausschalten!
5. Nach Abschluss automatisch Neustart.

---

## 6️⃣ Zigbee-Funktion prüfen

In der Konsole sollte erscheinen:

```
{"ZbState":{"Status":3,"Message":"Configured, starting coordinator"}}
{"ZbState":{"Status":40,"NewState":9,"Message":"Started as coordinator"}}
```

In der Weboberfläche erscheinen neue Menüpunkte:
- **Zigbee Permit Join**
- **Zigbee Map**

---

## 7️⃣ Zigbee-Geräte koppeln

1. Pairing aktivieren:
```bash
ZbPermitJoin 1
```
2. Zigbee-Gerät in Pairing-Modus setzen.
3. Nach erfolgreichem Pairing benennen:
```bash
ZbName 0x<ShortAddr> mein_geraetename
```

---

## ✅ Checkliste

- [ ] Gerät erfolgreich geöffnet & TTL-Adapter angeschlossen
- [ ] Tasmota32 geflasht
- [ ] WLAN konfiguriert
- [ ] Template gesetzt
- [ ] Berry-Skripte & HEX-Datei hochgeladen
- [ ] Zigbee-Koordinator erfolgreich geflasht
- [ ] Zigbee-Menüs sichtbar
- [ ] Geräte gekoppelt & benannt

---

## ℹ️ Hinweise

- Firmware und HEX-Dateien stammen aus den offiziellen Tasmota-Releases bzw. aus Community-Anleitungen (z. B. notenoughtech.com).
- Neuere `.hex`-Versionen können zusätzliche Geräteunterstützung bringen.
- Ein Backup der Konfiguration vor Updates ist empfohlen.
---

## 🔗 Wichtige Links & Downloads

- **Hauptanleitung & Dateien:**  
  [NotEnoughTech – Tasmota on Sonoff Zigbee Bridge Pro](https://notenoughtech.com/home-automation/tasmota-on-sonoff-zb-bridge-pro/)

- **Offizielle Tasmota-Projektseite:**  
  [https://tasmota.github.io](https://tasmota.github.io)

- **Tasmota Firmware (tasmota32-zbbrdgpro.factory.bin):**  
  [Direktdownload](https://ota.tasmota.com/tasmota32/release/tasmota32-zbbrdgpro.factory.bin)

- **Zigbee-Koordinator Firmware (SonoffZBPro_coord_YYYYMMDD.hex):**  
  [NotEnoughTech Download-Bereich](https://notenoughtech.com/home-automation/tasmota-on-sonoff-zb-bridge-pro/)  
  *(auf der Seite unter „Download Coordinator Firmware“ zu finden)*

- **Berry-Skripte:**  
  [intelhex.be (NotEnoughTech)](https://notenoughtech.com/home-automation/tasmota-on-sonoff-zb-bridge-pro/)  
  [sonoff_zb_pro_flasher.be (NotEnoughTech)](https://notenoughtech.com/home-automation/tasmota-on-sonoff-zb-bridge-pro/)

- **Partition Wizard für Tasmota:**  
  [Tasmota Partition Wizard.tapp (GitHub/Tasmota)](https://github.com/arendst/Tasmota/discussions)

- **esptool.py (Flashtool für ESP32/ESP8266):**  
  [GitHub – esptool](https://github.com/espressif/esptool)
