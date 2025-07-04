# Lernjournal: Webserver & Datenbank auf AWS EC2 einrichten

## Ziel
Ich möchte lernen, wie man auf einer AWS EC2-Instanz einen Webserver mit Datenbank aufsetzt, um eigene Webseiten und Anwendungen zu hosten.

## Schritt 1: EC2-Instanz starten

1. Zur AWS-Konsole navigieren: https://console.aws.amazon.com/ec2/
2. Auf "Instanz starten" klicken.
3. Ubuntu Server 22.04 LTS auswählen.
4. Instanztyp: `t2.micro` (kostenlos im Free Tier).
5. Key Pair erstellen (z. B. `webserver-key.pem`) und lokal speichern.
6. Sicherheitsgruppe konfigurieren:
   - Port 22 (SSH)
   - Port 80 (HTTP)
   - Optional: Port 3306 (MySQL) – nur intern oder mit IP-Beschränkung
7. Instanz starten und öffentliche IPv4-Adresse notieren.

## Schritt 2: SSH-Verbindung herstellen

```bash
chmod 400 webserver-key.pem
ssh -i "webserver-key.pem" ubuntu@<DEINE_PUBLIC_IP>
```

## Schritt 3: MariaDB (MySQL) Datenbank installieren

```bash
sudo apt update
sudo apt upgrade -y
sudo apt install mariadb-server -y
sudo mysql_secure_installation
```

Setup-Empfehlung:
- Passwort setzen: Ja  
- Anonyme Nutzer löschen: Ja  
- Root-Login beschränken: Ja  
- Testdatenbank löschen: Ja  
- Rechte neu laden: Ja

## Schritt 4: PHP installieren (für dynamische Inhalte)

```bash
sudo apt install php libapache2-mod-php php-mysql -y
```

Testdatei anlegen:

```bash
echo "<?php phpinfo(); ?>" | sudo tee /var/www/html/info.php
```

Im Browser aufrufen:  
`http://<DEINE_PUBLIC_IP>/info.php`

Erwartet: PHP Info-Seite

## Schritt 5: Test-Datenbank und Benutzer erstellen

```bash
sudo mysql -u root -p
```

Im SQL-Modus eingeben:

```sql
CREATE DATABASE beispiel;
CREATE USER 'tester'@'localhost' IDENTIFIED BY 'passwort123';
GRANT ALL PRIVILEGES ON beispiel.* TO 'tester'@'localhost';
FLUSH PRIVILEGES;
EXIT;
```

## Schritt 6: Aufräumen

```bash
sudo rm /var/www/html/info.php
```

## Ergebnis

- Webserver funktioniert unter `http://<PUBLIC_IP>`
- Datenbank ist eingerichtet und erreichbar
- PHP ist aktiv und kann mit MariaDB kommunizieren

## Reflexion

Ich habe heute gelernt, wie man eine AWS EC2-Instanz einrichtet und darauf MariaDB und PHP installiert.  
Besonders wichtig war die Sicherheitskonfiguration (SSH-Zugriff, Ports) und die Kontrolle über Root-Zugänge in der Datenbank.  
Jetzt kann ich eigene Webseiten hosten oder CMS wie WordPress installieren.

## Nächste Schritte

- HTTPS mit Let's Encrypt einrichten
- WordPress installieren
- Alternativ: Setup mit Docker
- Zugriffsrechte weiter absichern (z. B. mit Firewall oder Fail2Ban)
