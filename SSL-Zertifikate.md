# SSL-Zertifikate: Ein umfassender Guide

## 🔹 Grundlagen von SSL/TLS

SSL (Secure Sockets Layer) und sein Nachfolger TLS (Transport Layer Security) sind Protokolle zur sicheren Kommunikation über das Internet. Ein SSL-Zertifikat bestätigt die Identität einer Website und ermöglicht eine verschlüsselte Verbindung.

### Wichtige Begriffe:

- **CSR (Certificate Signing Request)**: Eine Anfrage für ein Zertifikat.
- **Private Key**: Ein geheimer Schlüssel, der zur Entschlüsselung der SSL-Kommunikation dient.
- **Public Key**: Der öffentliche Schlüssel, der im Zertifikat enthalten ist.
- **CA (Certificate Authority)**: Eine vertrauenswürdige Instanz, die SSL-Zertifikate ausstellt.

## 🔹 Erstellung eines SSL-Zertifikats

### 1. Generierung eines privaten Schlüssels und einer CSR

```bash
openssl req -new -newkey rsa:2048 -nodes -keyout domain.key -out domain.csr
```

### 2. Selbstsigniertes Zertifikat erstellen (für interne Nutzung)

```bash
openssl req -x509 -sha256 -days 365 -newkey rsa:2048 -keyout domain.key -out domain.crt
```

### 3. Ein von einer CA signiertes Zertifikat einbinden

Nach Erhalt der Datei von der CA (z.B. `domain.crt`):

```bash
sudo cp domain.crt /etc/ssl/certs/
sudo cp domain.key /etc/ssl/private/
```

## 🔹 Installation von SSL-Zertifikaten

### 1. Apache-Webserver (mod\_ssl erforderlich)

```bash
sudo a2enmod ssl
sudo systemctl restart apache2
```

#### Beispiel für eine Apache VirtualHost-Konfiguration:

```apache
<VirtualHost *:443>
    ServerName example.com
    SSLEngine on
    SSLCertificateFile /etc/ssl/certs/domain.crt
    SSLCertificateKeyFile /etc/ssl/private/domain.key
</VirtualHost>
```

### 2. Nginx-Webserver

```bash
sudo nano /etc/nginx/sites-available/default
```

Füge hinzu:

```nginx
server {
    listen 443 ssl;
    server_name example.com;
    ssl_certificate /etc/ssl/certs/domain.crt;
    ssl_certificate_key /etc/ssl/private/domain.key;
}
```

Speichern und Nginx neu laden:

```bash
sudo systemctl reload nginx
```

## 🔹 SSL-Zertifikate verwalten und überprüfen

### 1. Zertifikatsdetails anzeigen

```bash
openssl x509 -in domain.crt -text -noout
```

### 2. Ablaufdatum eines Zertifikats prüfen

```bash
openssl x509 -enddate -noout -in domain.crt
```

### 3. Zertifikat mit einer Website testen

```bash
openssl s_client -connect example.com:443 -servername example.com
```

## 🔹 Automatisierte SSL-Erneuerung mit Let's Encrypt

### 1. Certbot installieren

```bash
sudo apt update
sudo apt install certbot python3-certbot-nginx
```

### 2. SSL-Zertifikat für Nginx/Apache anfordern

```bash
sudo certbot --nginx -d example.com -d www.example.com
```

oder für Apache:

```bash
sudo certbot --apache -d example.com -d www.example.com
```

### 3. Automatische Erneuerung aktivieren

```bash
sudo certbot renew --dry-run
```

## 🔹 Fehlerbehebung

### 1. Prüfen, ob SSL korrekt eingerichtet ist

```bash
sudo ss -tlnp | grep 443
```

### 2. Fehlende Zertifikatskette beheben

Falls Browser über eine unvollständige Zertifikatskette warnen, muss das CA-Bundle ergänzt werden:

```bash
cat domain.crt ca-bundle.crt > fullchain.crt
```

### 3. SSL/TLS-Sicherheitsprüfung mit Qualys SSL Labs

```bash
https://www.ssllabs.com/ssltest/
```
