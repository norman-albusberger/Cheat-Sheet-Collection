# 📬 E-Mail-Zustellung & DNS-Konfiguration – Cheat Sheet

## 🧱 Grundlagen

| Authentifizierung | Zweck                                     | DNS-Typ | Beispiel                                                   |
|-------------------|-------------------------------------------|---------|------------------------------------------------------------|
| SPF               | Legt fest, welche Server Mails versenden dürfen | TXT     | `v=spf1 ip4:1.2.3.4 include:mailjet.com -all`              |
| DKIM              | Digitale Signatur der Mail                | TXT     | `v=DKIM1; k=rsa; p=MIGfMA0...`                             |
| DMARC             | Policy für SPF & DKIM                     | TXT     | `v=DMARC1; p=quarantine; rua=mailto:dmarc@deinedomain.de` |
| PTR (Reverse DNS) | Rückauflösung der Absender-IP             | PTR     | IP → `mail.deinedomain.de`                                |
| MX                | Empfangsserver für deine Domain           | MX      | `mail.deinedomain.de.` (mit Priorität)                    |
| A/AAAA            | IP-Adresse deines Mailservers             | A/AAAA  | `mail.deinedomain.de → 1.2.3.4`                            |

---

## ✅ Do's – Best Practices

### DNS & Authentifizierung

- ✅ SPF-Record setzen, **nur autorisierte IPs eintragen**
- ✅ DKIM-Signatur aktivieren und im DNS veröffentlichen
- ✅ DMARC mit `p=quarantine` oder `p=reject` aktiv setzen
- ✅ PTR-Eintrag korrekt (umgekehrte DNS-Auflösung zur Domain)
- ✅ `mail.`-Subdomain als FQDN im SMTP-HELO verwenden

### Mailserver-Verhalten

- ✅ TLS-Verschlüsselung aktivieren (STARTTLS / SMTPS)
- ✅ Authentifizierungspflicht für Mailversand einführen (SMTP Auth)
- ✅ Sendelimit pro Stunde setzen (z. B. max. 100 Mails)
- ✅ Logs aktiv überwachen (SPF-/DKIM-Fails, Bounces)
- ✅ Rate-Limiting und Greylisting implementieren

### Inhalte & Reputation

- ✅ HTML und Plaintext (Multipart) anbieten
- ✅ Klarer Betreff, kein Spam-Vokabular („100 % gratis“, „Dringend“, …)
- ✅ „List-Unsubscribe“-Header setzen (für Newsletter)
- ✅ Absender-Adresse sollte existieren und erreichbar sein
- ✅ Kein Versand über dynamische IPs

---

## ❌ Don'ts – Vermeidbare Fehler

- ❌ `p=none` dauerhaft bei DMARC (→ keine Policy → Spamgefahr)
- ❌ `~all` oder `+all` im SPF als Abschlusspolicy (statt `-all`)
- ❌ Mails mit unpassender `From:`-Adresse (z. B. Gmail-Absender von externem Server)
- ❌ Kein PTR → hohe Spam-Wahrscheinlichkeit
- ❌ Versand von mehreren Domains über dieselbe IP ohne passende Authentifizierung
- ❌ Anhänge ohne Kontext (z. B. ZIP ohne Erklärung) – landet oft im Spam

---

## 🔎 Tools zur Prüfung

| Tool                  | Funktion                                      |
|-----------------------|-----------------------------------------------|
| [mail-tester.com](https://www.mail-tester.com) | Vollständiger Spamtest inkl. Headeranalyse     |
| [mxtoolbox.com](https://mxtoolbox.com)         | Blacklists, SPF/DKIM/DMARC, MX-Prüfung         |
| [dmarcian.com](https://dmarcian.com)           | DMARC-Konformität & DNS Check                 |
| [Google Postmaster](https://postmaster.google.com) | Gmail-Zustellprobleme & Domain-Reputation     |
| [Microsoft SNDS](https://sendersupport.olc.protection.outlook.com) | Outlook/Hotmail-Reputation                    |

---

## 🛠 Beispielkonfiguration

### SPF
```txt
v=spf1 ip4:1.2.3.4 include:mailjet.com -all
