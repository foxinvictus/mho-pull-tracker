# MHO Pull-Tracker

Pull-Rechner und Sammlungs-Tracker für **Monster Hunter Outlands** (deutsche Version).
Rechnet alle Währungen in Spezial-Pulls um, zeigt die Chance auf den Spezial-Abenteurer, speichert deinen Stand online und vergleicht dich mit Freunden.

**Zur Website:** https://foxinvictus.github.io/mho-pull-tracker/

Aktuelle Version: **3.3 · Build 20** (alle Änderungen in der App unter *Einstellungen → Changelog*)

---

## Funktionen

### Rechner
Die Hauptseite ist in drei Bereiche gegliedert: **Vorrat** (was du gerade hast), **Banner** (Pity) und **Ausgegeben** (insgesamt gezogen).

- Rechnet **Purpurfedermünzen** (150:1), **Ruta-Münzen** (150:1) und **Spezial-Vorratsgutscheine** (50:1) in Spezial-Pulls um. Es zählen nur ganze Pulls, Reste werden angezeigt.
- Zeigt die **Chance auf den Spezial-Abenteurer** als Kurve: 50 % bei 90 Pulls, 100 % bei 120 Pulls, inklusive aktueller Pity.
- **„50/50 zuletzt verloren“**: Die Pity läuft ab dem verlorenen 50/50 weiter, die Garantie gibt es nach 90 Pulls.
- Ab der Garantie steht **100 %** und darunter, wie viele Pulls extra übrig sind.
- Welche Währungen umgetauscht werden, stellst du in den Einstellungen ein.
- **Zusätzliche Werte** (Einstellungen → Zusätzliche Werte) erscheinen direkt auf der Hauptseite:
  - **Standard-Vertrag** über dem Spezial-Vertrag
  - **Kumulative Werte** als Zeile ganz unten, nur mit Symbol: roter Brief = Spezial-Pulls gesamt, heller Brief = Standard-Pulls gesamt
- Das **ⓘ** beim Vorratsgutschein zeigt, wo du die Anzahl im Spiel findest.

### Verlauf
- **„Heutigen Stand speichern“** auf der Hauptseite trägt deine aktuellen Pulls mit Datum ein (ein Eintrag pro Tag).
- Gespeichert werden auch die **Standard-Verträge** und die **Gesamt-Pulls** (Spezial und Standard), wenn sie eingeschaltet sind.
- **„Verlauf“** zeigt die Kurve immer ab dem Release am 29.10.2026 mit 0. Umschalter:
  - **Verfügbar**: Spezial-Pulls und Standard-Verträge, die du gerade hast
  - **Ausgegeben**: wie viele Spezial- und Standard-Pulls du insgesamt gemacht hast
- **Ausgegeben pro Season**: Tabelle mit den Pulls je Season und der Gesamtsumme. So siehst du, ob du in einer Season mehr oder weniger gezogen hast.
- Gezogene Charaktere erscheinen als ★ an ihrem Tag, Season-Wechsel als senkrechte Linie.

### Sammlung
- Kachelübersicht aller SSR-Charaktere, sortiert nach Erscheinungsdatum und Version.
- **Antippen** wechselt den Status:
  - Spezial-Charaktere: Gezogen → Sparen → Skip → zurück
  - Standard-Charaktere: Gezogen an/aus
- Ein Charakter mit „Sparen“ wird auf der Hauptseite als **Ziel** mit Countdown angezeigt.

### Freunde vergleichen
- Über das **Freunde-Symbol** oben den Spielernamen eines Freundes eingeben → **Vergleichen**.
- Nebeneinander: Spezial-Pulls, Pity, Chance, gezogene SSR, Spar-Ziel und die komplette Sammlung (✓ gezogen · ★ sparen · Skip).
- Der höhere Wert ist mit ▲ markiert. Zuletzt verglichene Freunde bleiben als Schnellauswahl gespeichert.
- **Einstellungen → Freunde → „Meine Werte teilen“** ist standardmäßig an. Ausgeschaltet bist du für andere nicht mehr auffindbar.
- Teilen setzt ein Konto voraus. Geteilt werden nur Pulls, Pity, Chance, Sammlung und Verlauf, niemals die PIN.

### Konto
- Anmelden mit **Spielername + PIN** (6–8 Ziffern), ohne E-Mail.
- Dein Stand wird automatisch online gespeichert und auf jedem Gerät geladen.
- Ohne Konto funktioniert alles auch, dann bleibt der Stand nur auf dem Gerät.

---

## Bedienung in Kürze

| Symbol | Was es macht |
|---|---|
| ▦ (Kacheln) | Sammlung öffnen |
| 👥 (Personen) | Mit Freunden vergleichen |
| 👤 (Person) | Konto: anmelden, registrieren, abmelden |
| ⚙ (Zahnrad) | Einstellungen: Umtauschen, Teilen, zusätzliche Werte, Zurücksetzen, Changelog |

Der Punkt neben deinem Spielernamen zeigt den Speicherstatus:
gefüllt = online gespeichert · blinkt = speichert gerade · rot = gerade keine Verbindung (wird später nachgeholt)

---

## Pflege

### Neuen Charakter oder neues Banner eintragen
Die Charakter-Liste kommt aus dem Google Sheet, Tab **„Banner“**. Es reicht, dort eine neue Zeile einzutragen. Alle sehen sie beim nächsten Öffnen, ein neuer Upload ist nicht nötig.

| Spalte | Inhalt | Beispiel |
|---|---|---|
| Charakter | Name | Stylia |
| Typ | `Spezial` oder `Standard` | Spezial |
| Info | Element · Waffe · Banner | Eis · Bogen · Featured-Rekrutierung |
| Start | Startdatum | 27.11.2026 |
| Ende | Enddatum (leer = offen) | 24.12.2026 |
| Ende bestätigt | Haken, wenn offiziell | ☐ |
| Version | Spielversion oder Season | Season 0 |

Das Sheet muss für **„Jeder mit dem Link“ (Betrachter)** freigegeben sein.

### Neue Season eintragen
Tab **„Seasons“** im Google Sheet, eine Zeile pro Season:

| Season | Start | Ende |
|---|---|---|
| Season 0 (Pre-Season) | 29.10.2026 | 25.12.2026 |
| Season 1 | 26.12.2026 | *(leer, solange unbekannt)* |

Die Tabelle „Ausgegeben pro Season“ im Verlauf rechnet automatisch mit den neuen Zeiträumen.

### Neue Version der Website hochladen
1. Im Repo auf **Add file → Upload files**.
2. Die neue `index.html` hineinziehen (die alte wird ersetzt) → **Commit changes**.
3. Nach 1–2 Minuten die Seite mit **Strg+F5** neu laden.

Jede Änderung bekommt einen Eintrag im Changelog (`CHANGELOG` in `index.html`):
große Änderung = erste Zahl, kleine Änderung = zweite Zahl, Build = Anzahl aller Bearbeitungen.

---

## Technik

| Teil | Dienst |
|---|---|
| Website | GitHub Pages (eine einzelne `index.html`, keine Installation nötig) |
| Konten und Spielstände | Firebase Authentication + Cloud Firestore (Projekt `mho-pull-tracker`, kostenloser Spark-Plan) |
| Charakter-Liste und Seasons | Google Sheets (Tabs „Banner“ und „Seasons“) |

### Dateien im Repo
| Datei | Wofür |
|---|---|
| `index.html` | Die komplette Website inklusive Firebase-Konfiguration |
| `firestore.rules` | Sicherheitsregeln für die Datenbank (in Firebase unter *Firestore → Regeln* eingetragen) |
| `README.md` | Diese Beschreibung |

### Sicherheit
- Der Firebase-`apiKey` in `index.html` ist **kein Geheimnis**. Er identifiziert nur das Projekt und ist in der Google Cloud auf `https://foxinvictus.github.io/*` und die nötigen APIs (Identity Toolkit, Token Service, Cloud Firestore) eingeschränkt. Die GitHub-Warnung dazu ist als *False positive* geschlossen.
- Die Firestore-Regeln erlauben jedem Spieler nur Zugriff auf seinen eigenen Spielstand.
- Geteilte Werte (`profiles`) kann nur der Besitzer anlegen, ändern oder löschen. Andere können ein Profil nur einzeln über den Spielernamen abrufen, eine Liste aller Spieler gibt es nicht.
- **Nach Änderungen an `firestore.rules`** den Inhalt in der Firebase-Konsole unter *Firestore Database → Regeln* einfügen und veröffentlichen.
- Die PIN wird von Firebase verschlüsselt gespeichert. Nach zu vielen Fehlversuchen sperrt Firebase das Anmelden für eine Weile.

### PIN vergessen
Eine PIN lässt sich nicht zurücksetzen. Als Admin in der Firebase-Konsole:
1. *Firestore Database → players* → das Dokument mit dem passenden `name` suchen und die Dokument-ID merken.
2. Das Dokument löschen, ebenso unter *profiles* das Dokument mit demselben `name`.
3. Unter *Authentication → Nutzer* den Eintrag mit derselben Nutzer-UID löschen.

Danach kann sich der Spieler mit demselben Namen neu registrieren.

---

## Hinweis
Fan-Projekt ohne Verbindung zu Capcom oder TiMi Studio Group. Banner-Daten stammen aus offiziellen Ankündigungen und Community-Seiten. Enddaten ohne Bestätigung können sich ändern.
