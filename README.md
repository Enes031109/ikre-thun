# IKRE Thun – Vereinskasse

Webbasierte Kassenverwaltung für den Verein IKRE Thun.  
Gebaut mit React + Supabase. Läuft als einzelne HTML-Datei ohne Build-Prozess.

---

## Funktionen

**Admin**
- Übersicht über Einnahmen, ausstehende Zahlungen und Mitglieder
- Neue Zahlungen für Mitglieder erstellen
- Zahlungsbestätigungen von Mitgliedern prüfen und freigeben oder ablehnen
- Mitglieder verwalten (hinzufügen, bearbeiten, löschen)
- Neue Konten freigeben oder ablehnen

**Mitglieder**
- Eigene offene Zahlungen einsehen
- Zahlungen bestätigen (mit Betrag, Zahlungsart und Kommentar)
- Neue Zahlungen melden

---

## Technologie

| Schicht | Technologie |
|---|---|
| Frontend | React 18 (via CDN, kein Build nötig) |
| Datenbank | Supabase (PostgreSQL) |
| API | Supabase Edge Function (`db-proxy`) |
| Hosting | GitHub Pages |

---

## Lokale Entwicklung

Da die App eine einzelne HTML-Datei ist, reicht ein einfacher lokaler Server:

```bash
# Mit Python
python3 -m http.server 8080

# Mit Node.js (npx)
npx serve .
```

Dann im Browser öffnen: `http://localhost:8080`

---

## Datenbank-Schema

### `mitglieder`
| Spalte | Typ | Beschreibung |
|---|---|---|
| id | bigint | Primärschlüssel |
| name | text | Vollständiger Name |
| email | text | E-Mail (eindeutig) |
| password | text | Passwort |
| telefon | text | Telefonnummer |
| eintrittsdatum | date | Datum des Vereinseintritts |
| status | text | `ausstehend` / `aktiv` |
| created_at | timestamptz | Erstellungsdatum |

### `zahlungen`
| Spalte | Typ | Beschreibung |
|---|---|---|
| id | bigint | Primärschlüssel |
| datum | date | Fälligkeitsdatum |
| betrag | numeric | Geforderter Betrag (CHF) |
| bezahlt_betrag | numeric | Tatsächlich bezahlter Betrag |
| kategorie | text | z.B. Mitgliederbeitrag, Spende |
| zahlungsart | text | Twint / E-Banking / Bar |
| status | text | `ausstehend` / `pruefung` / `bestaetigt` / `abgelehnt` |
| kommentar_admin | text | Notiz des Admins |
| kommentar_mitglied | text | Notiz des Mitglieds |
| mitglied_id | bigint | Fremdschlüssel → mitglieder.id |
| created_at | timestamptz | Erstellungsdatum |

---

## Deployment

Die App wird automatisch über **GitHub Pages** bereitgestellt.  
Jede Änderung an `main` ist sofort live.

**Live-URL:** `https://DEIN-USERNAME.github.io/ikre-thun`

---

## Admin-Zugang (Demo)

```
E-Mail:   admin@ikrethun.ch
Passwort: admin123
```

> Den Admin-Zugangsdaten-Block aus dem Code entfernen bevor die Seite öffentlich geteilt wird.
