# Lernjournal LB3

## Tag 1 

- XAMPP installiert
- MySQL gestartet
- Systemvariable hinzugefügt (Pfad zur MySQL-Bin)
- Als root angemeldet und neuen Benutzer erstellt
- Rechte vergeben und mit neuem Benutzer getestet

### Datenbanksysteme vergleichen

| Produkt       | Vorteile                 | Nachteile                         | Anwendungen                |
|--------------|--------------------------|-----------------------------------|----------------------------|
| MariaDB      | Schnell, open source     | Weniger kommerzielle Tools        | Webanwendungen             |
| MySQL        | Weit verbreitet          | Kommerzielle Nutzung kostet       | LAMP, CMS                  |
| PostgreSQL   | Erweiterbar, stabil      | Komplexer Einstieg                | Geodaten, Forschung        |
| MS-SQL       | Gute Windows-Integration | Lizenzpflichtig, kaum Linux       | ERP, CRM                   |
 
---

## Tag 2 

- `my.ini` Datei angeschaut
- Konfigurationswerte kontrolliert (Port, Datenspeicherpfad)
- CSV-Dateien mit phpMyAdmin importiert
- Tabellenstruktur überprüft
- Daten korrekt geladen

---

## Tag 3 

- Tabelle `benutzer` zu InnoDB geändert
- Tabellentypen kontrolliert mit SQL
- `SHOW VARIABLES LIKE 'datadir'` benutzt
- Datenverzeichnis der DB überprüft

### Transaktionen getestet

- `BEGIN` gestartet, Daten geändert
- Auf anderem Client: Daten noch nicht sichtbar
- Nach `COMMIT` sichtbar
- `ROLLBACK` bringt alten Wert zurück

### Locking getestet

- Mit `LOCK TABLES` Tabelle gesperrt
- Zweite Session konnte nicht zugreifen
- Bei InnoDB `SELECT ... FOR UPDATE` gemacht
- Row-Level-Locking funktioniert wie erwartet

---

## Tag 4 

- Benutzer erstellt mit verschiedenen Hosts
- `user_local`, `user_remote1`, `user_remote2`, `user_host`
- `SELECT * FROM mysql.user` kontrolliert
- Verbindung über IP und Domain getestet
- Passwort geändert mit `ALTER USER`
- Host geändert durch direktes Update in DB

---

## Tag 5 

- Rollen in MySQL erstellt
- Rechte an Rollen vergeben (SELECT, INSERT, usw.)
- Rolle einem Benutzer zugewiesen
- Rolle temporär aktiviert mit `SET ROLE`
- Unterschied zwischen Standardrolle und Sitzungsrolle getestet
