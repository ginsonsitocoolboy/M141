# Projekt LB3

# 1. Teil Lokale Datenbank mit MySQL XAMPP

## 1. Lokale Datenbank

Ich habe MySQL mit XAMPP benutzt, um die Datenbank lokal zu testen. MySQL ist einfach zu verwenden und läuft gut auf dem lokalen Server.

---

## 1.1 Zugriffsmatrix

In der Zugriffsmatrix steht, wer was in der Datenbank machen darf. Zum Beispiel:

- Admin: darf alles
- Mitarbeiter: darf z.B. Buchungen sehen und ändern
- Gast: darf nur Länder und Leistungen sehen

---

## 1.2 Zugriffsrechte

Ich habe Benutzer in MySQL erstellt und ihnen Rechte gegeben, wie in der Zugriffsmatrix. Dafür habe ich SQL-Befehle geschrieben und sie in mySQL ausgeführt.

Ich habe auch getestet, ob die Benutzer nur das dürfen, was sie dürfen. Die Tests habe ich dokumentiert.

---

## 1.3 Daten importieren und bereinigen

Ich habe CSV-Dateien mit mySQL in die Datenbank importiert. Danach habe ich Fremdschlüssel, Indizes und Regeln ergänzt, damit alles richtig funktioniert.

---

## 1.4 Testen

Ich habe geprüft, ob die Daten stimmen, also keine Fehler enthalten. Zusätzlich habe ich Testdaten eingefügt, um für eine spätere Migration vorbereitet zu sein.


---

## Fazit von der lokalen Datenbank

Die Datenbank läuft lokal mit MySQL. Alle Daten sind korrekt drin, die Benutzerrechte stimmen und alles wurde getestet. Damit ist die Basis für die Migration in die Cloud bereit.

# 2. Teil Remote Cloud-Datenbank 

## 2.1 Setup Cloud-DBMS

Ich habe eine MariaDB-Datenbank in der Cloud (z.B. auf AWS) eingerichtet. Dazu gehörte:

- Server starten (z.B. EC2 auf AWS)
- mySQL installieren
- Port 3306 öffnen, damit man auf die Datenbank zugreifen kann
- Benutzer anlegen und Verbindung testen

---

## 2.2 Betrieb

Die Datenbank wurde so eingerichtet, dass sie für den echten Einsatz (Produktion) sicher ist.

- Externe Zugriffe nur über bestimmte IPs erlaubt
- Konfigurationsdateien (.ini) angepasst, z.B. für Logs und Sicherheit

Alles läuft stabil und ist bereit für die weitere Nutzung oder Migration.

# 3. Teil Automatisierte Migration von lokal zu Cloud

## 3.1 Berechtigungen übertragen

Ich habe die Benutzerrechte (Zugriffsberechtigungen) von der lokalen Datenbank in die Cloud-Datenbank übertragen.

- Mit SQL-Skripts (DCL) wurden alle Rechte automatisch gesetzt
- Die Benutzer wurden getestet
- Ich habe aufgeschrieben, ob die Rechte richtig funktionieren

---

## 3.2 Daten übertragen

Die Datenbankstruktur (Tabellen usw.) und die Inhalte wurden automatisch von lokal in die Cloud übertragen.

- Mit SQL-Skripten (DDL und DML)
- Danach habe ich Fremdschlüssel, Indizes und Regeln ergänzt, damit alles korrekt ist
---

## 3.3 Testen

Ich habe geprüft, ob alle Daten richtig übertragen wurden. Dazu habe ich Testdaten aus der lokalen DB genommen und mit der Cloud-Version verglichen.

-- Testfall 1: Verbindung zur Datenbank
-- (Wird ausserhalb des SQL-Clients getestet – z. B. über Bash)
-- Beispiel: mysql -h <host> -u <user> -p

---
 
-- Testfall 2: Tabelle 'tbl_personen' vorhanden?
SHOW TABLES LIKE 'tbl_personen';

---
 
-- Testfall 3: Stichprobe – Ist ein bestimmter Datensatz korrekt da?
SELECT * FROM tbl_personen 
WHERE nachname = 'Muster' AND vorname = 'Max';

---
 
-- Testfall 4: Zeilenanzahl überprüfen – Stimmen Anzahl vor/nach Migration?
SELECT COUNT(*) AS anzahl_personen FROM tbl_personen;

---
 
-- Testfall 5: Sonderzeichen / Zeichencodierung korrekt?
SELECT vorname, nachname 
FROM tbl_personen 
WHERE nachname LIKE '%ü%' OR nachname LIKE '%ß%';

---
 
-- Testfall 6: Fremdschlüsselprüfung – Gibt es verwaiste Einträge?
SELECT * 
FROM tbl_buchungen 
WHERE personen_id NOT IN (SELECT id FROM tbl_personen);

---
 
-- Testfall 7: Benutzerrechte – Prüfen ob Zugriffsmatrix korrekt umgesetzt wurde
SHOW GRANTS FOR 'backoffice'@'%';

---
 
-- Testfall 8 (optional): Gibt es NULL-Werte in Pflichtfeldern?
SELECT * 
FROM tbl_personen 
WHERE vorname IS NULL OR nachname IS NULL;

---
 
-- Testfall 9 (optional): Sind Datumsangaben korrekt formatiert?
SELECT geburtsdatum 
FROM tbl_personen 
WHERE geburtsdatum NOT BETWEEN '1900-01-01' AND CURDATE();

- Abfragen für Datenkonsistenz erstellt
- Ergebnisse dokumentiert


# Fazit 

Wir sind mit allem relativ knapp durchgekomm und haben all unsere Ziele erreicht. Ausserdem haben wir auch gelernt von diesem Projekt.

